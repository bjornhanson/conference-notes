# Disney's Room Detective - A Real World JavaScript IoT Solution

Speaker
- [Garth Henson](https://github.com/guahanweb), technical lead for an Emerging Technologies team at The Walt Disney Company's Seattle office
- Works for Enterprise Technology (DTSS), working on a lot of proof-of-concept projects, basically as a design/tech services group

### The Problem

They have a problem at his 7-story, ~700-person Seattle office where sometimes meeting rooms are all booked, but half are empty. What if you just need a space and a whiteboard for 10 minutes?

Main issue: is a room physically occupied or not

### Goal

Have a live, interactive map of each floor that shows rooms that are occupied or open

### Workflow
```
Sensors --> State Manager --> Metadata --> WebSocket --> Web App
-------     ----------------------------------------     -------
 room                        server                      browser
```

### Solution

Used Rapsberry Pis running Node connected to PIR (motion) sensors (something like [this](https://www.sparkfun.com/products/13285))

### Software Stack
- Raspberry Pi
- Node.js
- MongoDB
- Google Cloud Platform
- redis
- WebSockets
- Angular

### Example Code
```javascript
var gpio = require('onoff').Gpio;
var pir = new gpio(4, 'in', 'both');

pir.watch((err, value) => {
  if(!value) {
    // Do something
  } else {
    // Do something else
  }
})
```

```javascript
var state = INACTIVE;
var inactive_ttl = 120000;
var timeout;

PIR.on('activity', () => {
  if (timeout !== null) {
    clearTimeout(timeout);
  }

  if (state === INACTIVE) {
    state = ACTIVE;
  }
});
```

```javascript
PIR.on('inactivity', () => {
  // Do stuff...
})
```

### Deployment
- CI/CD using [Distelli](https://www.distelli.com) to push new changes to fleet of Pis
- Also used Docker and Google App Engines

## Resources
- [Tech @ Disney](https://www.youtube.com/watch?v=2hbmxORF328) video
- [onoff](https://github.com/fivdi/onoff) GPIO access and interrupt detection Node.js library
- [Shodan](https://www.shodan.io) IoT device search engine (for finding insecure devices)
- [Distelli](https://www.distelli.com) fleet management for deploying new code
