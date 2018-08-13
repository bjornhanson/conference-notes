# Using JavaScript to write Native Applications/SDKs for iOS, Android, and the Web
- Speakers: Siddharth Reddy Malk (@msiddharthreddy), Derek Anderson (@dmikeyanderson) (PayPal)
- [Slides](https://www.slideshare.net/DerekAnderson20/using-javascript-to-write-native-mobile-applications)

## Notes

They work on PayPal checkout (used to pay for things on mobile apps/web)

Why JS?
- It's awesome (not a legit reason)
- Rapid development cycle
- Dynaically updateable UIs on mobile (like on the web) - can point mobile app to CDN to pull latest JS, enabling A/B testing, fast updates, etc.
- Less friction with merchants

Why React Native? (started wit this)
- Large ecosystem & large community
- Multi-platform (iOS, Android, Windows)
- Common JS design (ES Classes, JSX via Babel)
- Easily extendable natively
- Dynamically updateable (without need for rebuilding native code)

What didn't work with React Native
- React Native's really fast release cycle (thing changed a lot)
- Integration as an SDK wasn't the best
- Already big, grew heavier over time
- 2nd and 3rd party developers were apprehensive (said it was really painful to use)
- Too many libraries, hard to internalize, required npm to distribute
- Ambotious, bloated
- Release cycle was too fast

The PayPal engineering team developed Syr to improve upon React Native:
- Using componenets and JSX
- Easy to write and integrate native modules (iOS, Android)
- UI still in JS, so that can be hosed on a remote server
- Syr-Push (one of the best parts)
  - Deterministic chunking using Webpack
  - Incremental diffing for patches

Why is Syr better than React Native?
- Doesn't use JSC (kinda sucks), uses native JS engine
- Host platform first approach
  - Consistent performanc no longer an issue
  - Built-in use of JavaScript bridges
  - Uses native componenets and no DOM
  - Can use Chrome, Safari, or Firefox dev tools to debug

## Resources
- https://syr.js.org/
- @syr_js
