###### NOTE: This contains ***my*** some tricks and shortcuts for Javascript
## Contents
* [Async try await catch - Funtion based](#async-try-await-catch---funtion-based)
* [Service Worker Code for PWA](#service-worker-code-for-pwa)


---

### Async try await catch - Funtion based
This allows me to avoid the callback functions and work as single **Function**.

```javascript
/**
    * Inspired from Jeff Delaney -> https://youtu.be/ITogH7lJTyE
    * Returns [error,data] by resoleving the Promise Externally using one try catch
    * 
    * @param {promise} promise, the promise to be resolved.
    * @return {array} [error,data], if catch block raise any error returns [error,null] else [null,data]
*/
async function resolvePromise(promise) {
    try {
        const data = await promise;
        return [null, data];
    } catch (error) {
        return [error, null];
    }
}
```

###### Example - With simple Fetch call.
```javascript
async function mytest () {
    const [err1,response] = await resolvePromise(fetch("http://jsonplaceholder.typicode.com/albums"));
    const [err2, data] = await resolvePromise(response.json());
    console.log(data) // Contains the Data
}
```


---

### Service Worker Code for PWA
This is one time look up for creating service worker file for PWA

```javascript

// version - 1.0
const CACHE_NAME = 'site-static-v1';
const assets = [
    '/',
    '/index.html'
    // Contains the Cache Pages
    // one offline Page
];

// install event
self.addEventListener('install', event => {
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then(cache => {
                cache.addAll(assets);
            })
    )
})

// activate event
self.addEventListener('activate', event => {
    event.waitUntil(
        caches.keys().then(keys => {
            return Promise.all(keys
                .filter(key => key!==CACHE_NAME)
                .map(key => caches.delete(key))
                );
        })
    )
})

// fetch event
self.addEventListener('fetch', event => {
    event.respondWith(
        caches.match(event.request).then(res => res || fetch(event.request)
        .catch(() => caches.match("/pages/fallback.html"))
        )) // Ofline Page Goes Here
})

```
