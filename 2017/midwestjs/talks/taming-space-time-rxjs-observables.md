# Taming Space and Time with RxJS Observables

Speaker
- [Jeff Barczewski](https://github.com/jeffbski)
- [His Midwest JS Talks](https://codewinds.com/mwjs2017)
- [Slides for this talk](https://codewinds.com/assets/article/midwestjs-2017-rxjs-slides.pdf)

Observables (vs Promises)
- Zero to many values over time
- Cancellable
- Synchronous or asynchronous
- Composable streams
- Observables can wait for subscribe to start
- RxJS provides large set of operators

## Examples (more in slides)

Observables

```javascript
const ob$ = Rx.Observable.create(obs => {
  obs.next(10); // send first value
  obs.next(20); // 2nd
  obs.next(30); // 3rd
  obs.complete(); // we are done
});

ob$.subscribe(x => console.log(x));
// 10, 20, 30
```

Observable Errors

```javascript
const ob$ = Rx.Observable.create(obs => {
  obs.next(10); // send first value
  obs.next(20); // 2nd
  obs.error(new Error('something bad'));
});
ob$.subscribe(
  x => console.log(x), // next
  err => console.error(err), // errored
  () => console.log('complete') // complete
);
```

Observable.ajax

```javascript
const ob$ = Rx.Observable.ajax.getJSON('https://reqres.in/api/users')
  .map(payload => payload.data); /* use data prop */

ob$.subscribe({
  next: x => console.log('next', JSON.stringify(x, null, 2)),
  error: err => console.log('error', err),
  complete: () => console.log('complete')
});
// next [{ id: 1, first_name: 'george'...
//   { id: 2, first_name: 'lucille'...
//   ...
// complete
```


Observable.webSocket

```javascript
const wsSubject = Rx.Observable.webSocket({
  url: 'ws://localhost:8010',
  // WebSocketCtor: WebSocket, // only for Node.js, import WebSocket from 'ws';
  resultSelector: x => x.data // default is JSON.parse(x.data)
});

wsSubject.next('foo'); // queue foo for sending
wsSubject.next('bar'); // queue bar for sending

// connect to websocket, send queued msgs, listen for responses
wsSubject.subscribe(
  x => console.log('received', x),
  err => console.error('error', err),
  () => console.log('done')
);
```

## Resources
- http://rxmarbles.com
- [RxJS Tutorial](http://reactivex.io/rxjs/manual/tutorial.html)
- [RxJS](http://reactivex.io/rxjs/) (RxJS is JavaScript version of ReactiveX)
