# The Internet of JavaScripty Things: Control Bluetooth Devices with your Browser

- Speaker: [Matt Steele](https://github.com/mattdsteele), software engineer at Union Pacific Railroad
- Slides: http://matt.steele.blue/web-bluetooth

## Bluetooth Devices
- Unfortunately, random, cheap Bluetooth devices all have their own sketchy apps

## Example Code

Scan for services (ex: the battery service)
```javascript
if ('bluetooth' in navigator) {
  navigator.bluetooth.requestDevice({
    filters: [{
      services: [
        'battery_service'
      ]
    }]
  });
}
```

UUIDs
```javascript
if ('bluetooth' in navigator) {
  navigator.bluetooth.requestDevice({
    filters: [{
      services: [
        '28998e03-c277-48a8-91cb-b29ab0f01ac4'
      ]
    }]
  });
}
```

Log device name
```javascript
navigator.bluetooth.requestDevice({
  filters: [{
    services: [ '28998e03-c277-48a8-91cb-b29ab0f01ac4' ]
  }]
})
.then(device => {
  console.log(device.name);
});
```

Getting down into the raw data
```javascript
.then(device => device.gatt.connect())
.then(server => server.getPrimaryService('battery_service'))
.then(service => service.getCharacteristic('battery_level'))
.then(characteristic => characteristic.readValue())
.then(value => {
  console.log(`Battery level is ${value}%`); // <-- Uint8Array!
})
.catch(e => { console.error(e) });
```

Using async/away to clean it up
```javascript
try {
  const server = await device.gatt.connect();
  const service = await server.getPrimaryService('battery_service');
  const characteristic = await service.getCharacteristic('battery_level');
  const value = await characteristic.readValue();
  console.log(`Battery level is ${value}%`); // <-- Uint8Array!
} catch(e) {
  console.error(e);
}
```

One-time read
```javascript
characteristic.addEventListener('characteristicvaluechanged', event => {
  const value = event.target.value;
  console.log(value);
});
```

Notifications/indications from multiple reads
```javascript
await characteristic.startNotifications();
characteristic.addEventListener('characteristicvaluechanged', event => {
  const value = event.target.value;
  console.log(value);
});
});
```

Getting heart-rate
```javascript
const device = await navigator.bluetooth.requestDevice({
  filters: [{ services: ['heart_rate'] }]
});
const server =  await device.gatt.connect();
const service = await server.getPrimaryService('heart_rate');
const characteristic = await service.getCharacteristic('heart_rate_measurement');
await characteristic.startNotifications;
characteristic.addEventListener('characteristicvaluechanged',
  handleCharacteristicValueChanged);
```

May have to convert endian-ness (using second argument as `true` for `getUint16` function) from some devices
```javascript
char.addEventListener('characteristicvaluechanged', e => {
  const { value } = e.target;
  console.log(value.getUint16(12, true)));
});
```

Writing data
```javascript
const command = new Uint8Array([0xa, 0x5, 0x3, 0x4]);
await characteristic.writeValue(command);
console.log('Wrote a value');
```

Example of writing color to an [Elfy](http://en.emie.com/emie-elfy-smart-light) smart light
```javascript
async writeColors(r, g, b) {
  const colors = [r, g, b]
    .map(e => e / 16)
    .map(e => Math.floor(e));
  // aa 16 0r 0g 0b
  const command = new Uint8Array([0xaa, 0x16].concat(colors));
  const service = await this.device.gatt.getPrimaryService('6e402001-b5a3-f393-e0a9-e50e24dcca9e');
  const characteristic = await service.getCharacteristic(  '6e402002-b5a3-f393-e0a9-e50e24dcca9e');
  await characteristic.writeValue(command);
}
```

Raw data from bike cycling speed sensor
```javascript
const server = await this.device.gatt.connect();
const service = await server.getPrimaryService('cycling_speed_and_cadence');
this.char = await service.getCharacteristic('csc_measurement');
await this.char.startNotifications();
fromEvent(this.char, 'characteristicvaluechanged')
.map(({ target: { value } }) => {
  return value;
});
```

Examples of parsing data
```javascript
parsedMeasurement$() {
  return fromEvent(this.char, 'changed')
  .map(({ target: { value } }) => value )
  .map(data => {
    const flags = data.getUint8(0);
    const wheelDataPresent = flags & 0x1;
    const crankDataPresent = flags & 0x2;
```

```javascript
const output = {};
if (wheelDataPresent) {
  const revs = data.getUint32(1, true);
  const lastWheel = data.getUint16(5, true) / 1024;
}
```

```javascript
parsedCadence$() {
  const cadence$ = this.parsedMeasurement$()
  .map(({ totalCrankRevolutions, lastCrankTime }) => {
    return { totalCrankRevolutions, lastCrankTime }
  })
  .compose(pairwise)
  .map(([prev, curr]) => {
    const revDelta = curr.totalCrankRevolutions - prev.totalCrankRevolutions;
    const timeDelta = curr.lastCrankTime - prev.lastCrankTime;
    return { revDelta, timeDelta };
  })
  .map(({ revDelta, timeDelta}) => {
    const minuteRatio = 60 / timeDelta;
    return revDelta * minuteRatio;
  });
}
```

```javascript
parsedSpeed$() {
  .map(({ revDelta, timeDelta}) => {
    const wheelSize = 622; // mm; 700C
    const wheelCircumference = Math.PI * wheelSize;
    const rpm = revDelta * (60 / timeDelta);
    const rph = rpm * 60;
    const mmph = rph * wheelCircumference;
    const kph = mmph / 1e6;
    return kph;
  });
}
```

## Resources
- [Blog post by Matt](https://steele.blue/web-bluetooth) about his talk on Web Bluetooth, including links to his code on GitHub
- [Matt's presentation and demos](https://github.com/mattdsteele/web-bluetooth) on GitHub
- [meh.com](http://meh.com) daily deals with hilarious descriptions, easy to acquire lots of cheap, random Bluetooth devices
- [Interact with Bluetooth devices on the Web](https://developers.google.com/web/updates/2015/07/interact-with-ble-devices-on-the-web) on Google Developers
- [General Attributes](https://www.bluetooth.com/specifications/gatt) specifications on bluetooth.com
- [Web Bluetooth browser support](http://caniuse.com/#search=Web%20Bluetooth) on caniuse.com
- [An introduction to the Web Bluetooth API](https://dev.opera.com/articles/web-bluetooth-intro/) on Dev.Opera
- [BB-8 Control Web Bluetooth demo](https://github.com/operasoftware/bb8) repo on GitHub
- [Wireshark can be used](https://wiki.wireshark.org/Bluetooth) for looking at Bluetooth traffic
