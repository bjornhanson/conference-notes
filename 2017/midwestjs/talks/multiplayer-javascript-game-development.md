# Multiplayer JavaScript Game Development

- Speaker: [Jeremy Lund](https://github.com/lund0n), principal engineer at Workfront
- [Barnyard Basic](http://github.com/lund0n/barnyard) repo for game that was used in presentation
- [Slides](https://docs.google.com/presentation/d/1Ib80GSRHJDP5fhUyfSO7bTaHvbba2hYvB9Hyie2B5rM/edit)

## Highlights
- Games are fun

## Software Stack
- Native browser APIs (Canvas, WebSockets)
- [ws](https://github.com/websockets/ws) (for server WebSocket code)
- RxJS
- Math

## Observables
- "A set of values that arrive over time"
- Good at capturing state (like game state)

## Goal - What are we building?
- `Barnyard`: Tron meets cute emoji animals

## Architecture
```
Intent --------------> Model ------------> View

User input           Series of            Draw on
and game loop        reducers             canvas
```

Model is on server (includes stuff like collission detection)

## Implementation
- Canvas element ((0,0) is upper left, (`canvas.width`, `canvas.height`) is bottom right)
- `Observable.of` that returns initial game state (first marble on marble diagram)
- `Observable.merge`
- Just used animal emoji, so no special graphic assets (drawn using `fillText` function)
- `Observable.interval` used for game rate
- Used `Observable.pairwise()`...
- Used `Observable.let`
- `Observable.sample` to not have keyboard events overwhelm animation rate
- Store initial point and then turn point coordinates in array for collission detection
- Different ideas of collission detection, basic idea is you have a bounding boxes of two elements and see if they overlap
- To add server with WebSocket, basically moved startup code to server and do it for new
- Used `Observable.webSocket`

```javascript
const gameRate = (frameRate = 60, scheduler = Scheduler.animationFrame) =>
  Observable.interval(1000 / frameRate, scheduler).map(() => scheduler.now())
```

Example - getting keycode with RxJS
```javascript
const keyCode = Rx.Observable.fromEvent(document, 'keydown').pluck('keyCode');
keyCode.subscribe(x => console.log(x), e => console.error(e));
```

## Resources
- [Barnyard Basic](http://github.com/lund0n/barnyard) repo for game that was used in presentation
- [Slides](https://docs.google.com/presentation/d/1Ib80GSRHJDP5fhUyfSO7bTaHvbba2hYvB9Hyie2B5rM/edit)
- learnrxjs.io
- devdocs.io
- Gamkedo YouTube channel
- Js13kgames.com - make your own game in 13k or less
- [Now](https://zeit.co/now) for deployment in demo
