# Marble-Driven Development with RxJS
- RxJS maintained by Netflix
- Speaker: [Eric Ponto](https://github.com/ericponto), front end developer at Principal Financial Group
- [Slides](http://slides.ericponto.com/mwjs-mdd/#/)

## Observable
- Representation of any set of values over any amount of time (the most basic building block of RxJS)
- Has `next`, `error`, `complete`
- Observable. [`of`, `from`, `fromPromise`]
- Like Promise objects that you can resolve multiple times
- Is like an Iterable that pushes the next value to you
- Like an Array whose values are separated by time, rather than by value
- Temporal, like Promise object, but plural (like arrays):

|          | Singular | Plural         |
| ---------|----------|----------------|
| Spatial  | Value    | Array/Iterable |
| Temporal | Promise  | Observable     |

Example:

```javascript
const x = Observable.interval(1000)
const total = timer.scan(
  (accumulator, item) => accumulator + item
  , 0
)
total.subscribe(console.log)
```


Marble diagrams
- Learning to read/use marble diagram will help in learning how observables work
- If you can make a marble diagram for it, you can use RxJS for it

## Marble-driven development
  1. [Diagram the requirements](http://slides.ericponto.com/mwjs-mdd/#/84)
  2. [Use diagrams to write tests](http://slides.ericponto.com/mwjs-mdd/#/86) (Most RxJS examples use Jasmine for testing, but he thought he'd be different and use QUnit)
  3. [Use learned RxJS to develop app](http://slides.ericponto.com/mwjs-mdd/#/88)

```
----a-------b--------#----------|
   next    next    error    complete
```

## Resources
- http://slides.ericponto.com/mwjs-mdd/#/
- ["General Theory of Reactivity" essay](https://github.com/kriskowal/gtor)
- http://reactivex.io/rxjs
- http://rxmarbles.com
- http://rxviz.com
- http://rxfiddle.net
