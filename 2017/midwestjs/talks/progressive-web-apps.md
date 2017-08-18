# Leverage the power of native with Progressive Web Apps

Speakers
- [Abraham Williams](https://github.com/abraham), experienced developer, start-up founder, international speaker, senior developer at Bendyworks, top 1% contributor at Stack Overflow and an active member of Google Developer
- [Pearl Latteier](https://github.com/pearlbea), software engineer at Bendyworks (in Madison, WI)

[Presentation Slides](https://docs.google.com/presentation/d/1TybgcgjmAFB8AHTOQzBMrKOc4XAma-HFEvdWqdXUOQc/edit)

[Progressivew Web App Demo](http://pwa.sprinkle.space) and [source](https://github.com/abraham/sprinkle)

## What are PWAs
- Fast (60fps, jank-free, 3-second meaningful paint)
- Secure (HTTPS)
- Responsive
- Native benefits (installable, available offline, engaging)

## Why are PWAs Awesome?
- Cheaper and easier than making multiple native apps
- Built with familiar web technologies
- Improve user experience on spotty connections
- Reach out of the web to engage users

## Service Workers
- Cache app layout resources
- Intercept network requests
- Handle push notifications

Example Code
```javascript
// registering a service worker
if(navigator.serviceWorker){
  navigator.serviceWorker
    .register('serviceworker.js')
    .then(registration => {
      console.log('Registered');
  });
}
```

```javascript
this.addEventListener('install', event => {
  console.log('Installed');
});
```

## Caching App Shell
Allows you to render the app shell immediately before content is loaded, making the experience feel more instantaneous (after initial load)

Example Code
```javascript
const CACHE_VERSION = 'v1';
const APP_LAYOUT_FILES = [
  '/',
  '/js/app.js',
  '/js/material.min.js',
  '/css/material.blue-red.min.css'
];

this.addEventListener('install',event => {
  let waitPromise = caches.open(CACHE_VERSION)
    .then(cache => {
      // Want to use addAll here so all or nothing (if any fail, none load)
      return cache.addAll(APP_LAYOUT_FILES);
    });
  event.waitUntil(waitPromise);
});
```

## Offline Data
Service Workers can use the `fetch` event to intercept app network requests.

Code Example
```javascript
this.addEventListener('fetch', event => {
  let responsePromise = caches.match(event.request)
    .then(response => {
      // If have it cached, just return that to browser instead of doing request
      if (response) { return response; }

      // Request data from server if it's not cached
      return fetch(event.request)
        .then(response => {
          return response;
        });
    });
  event.respondWith(responsePromise);
});
```

## Caching Strategies
- Cache only
- Cache first, network fallback
- Cache first and network update (if data on server is newer, change it or notify user)
- Network only
- Network first, cache fallback

## Tools
- Workbox ([GitHub](https://github.com/GoogleChrome/workbox), [website](https://workboxjs.org))
- Chrome Dev Tools > Application > Service Workers

## Web Push API
1. Get Permissions to Send Push Notifications
2. Get PushSubscription
3. Send PushSubscription to Your Server

Code Example - asking permission (gives access to both browser API and PushSubscription...?)
```javascript
Notification.requestPermission()
  .then(result => {
    if (result === 'denied') {
      console.log('Permission denied');
      return;
    }
    // User has allowed push notifications
  });
```

Code Example - send PushSubscription details to server
```javascript
getSWRegistration()
  .then((registration) => {

    const opts = { … };

    return registration.pushManager
                       .subscribe(opts);
  });

// Send PushSubscription details to server (maybe store key with user data, possibly
// associate it with the particular thing they were requesting)
```

```
                 Web Push
              Protocol Request                           Message Arrives
Your Server ---------------------> Push Service ------->  on the Device
```

Using WebPush Node Library on server
```javascript
// PushSubscription details from client

webPush.sendNotification(
  pushSubscription,
  Payload
);
```

```
Message arrives         Browser wakes             Push event
on device      -----> up service worker ------> is dispatched
```

```javascript
this.addEventListener('push',event => {
  let title = 'Push message';
  let waitPromise = this.registration
    .showNotification(title, {
      body: 'The Message',
      icon: 'images/icon.png',
      tag: 'my-tag'
    });
  event.waitUntil(waitPromise);
});
```
## Manifest
Can just use [this generator](https://brucelawson.github.io/manifest/
) to make it easily

Have this in your HTML page
```HTML
<link rel="manifest" href="/manifest.json">
```

Example `manifest.json`
```javascript
{
  "name": "Sprinkle PWA Demo",
  "short_name": "Sprinkle",
  "description": "Example PWA",
  "start_url": "/",
  "background_color": "#2196f3",
  "theme_color": "#2196f3",
  "display": "standalone",
  "icons": [
    {
      "src": "/icons/gallery-256x256.png",
      "sizes": "256x256",
      "type": "image/png"
    }
  ]
}
```

## When are PWAs Coming?

Browsers that support PWAs:
- Chrome
- Firefox
- Opera

Browsers that will support them soon:
- Edge (can be enabled with flags)
- Safari

## Be smart, check for browser support
```javascript
// Be progressive: check for support

if(‘serviceWorker’ in navigator) {
  console.log(‘Yay! Service Workers’);

  if(‘PushManager’ in window) {
    console.log(‘Also Push API’);
  }
}
```

## Offline Data Storage
Service Workers have access to indexDB

## Resources
- [Presentation Slides](https://docs.google.com/presentation/d/1TybgcgjmAFB8AHTOQzBMrKOc4XAma-HFEvdWqdXUOQc/edit)
- [Progressivew Web App Demo](http://pwa.sprinkle.space) and [source](https://github.com/abraham/sprinkle)
- Workbox ([GitHub](https://github.com/GoogleChrome/workbox), [website](https://workboxjs.org)) Google libraries for progressive web app offline caching
- PWA Rocks [website](https://pwa.rocks) and [GitHub repo](https://github.com/pwarocks/pwa.rocks) (check out pull requests) is nice collection of PWAs maintained by Opera developers
- [Service Worker Lifecycle](https://developers.google.com/web/fundamentals/primers/service-worker/service-worker-lifecycle)
) on Google Developers
- [Progressive Web Apps Checklist](https://developers.google.com/web/progressive-web-apps/checklist
) on Google Developers
- [Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
) on Mozilla Developers
- [How Push Works](https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/how-push-works)
) on Google Developers
- [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) handles push notifications easier
- [Manifest Generator](https://brucelawson.github.io/manifest/)
)
- [Service Workers support](http://caniuse.com/#feat=serviceworkers) on caniuse.com
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) audit tool
- [Service Worker Cookbook](https://serviceworke.rs)
- https://github.com/WICG/BackgroundSync/blob/master/explainer.md
- https://developer.mozilla.org/en-US/docs/Web/API/Push_API
- https://developer.mozilla.org/en-US/docs/Web/Manifest
- https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/
- https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/
- https://msdn.microsoft.com/en-us/library/hh772406(v=vs.85).aspx
- https://codelabs.developers.google.com/?cat=Web
