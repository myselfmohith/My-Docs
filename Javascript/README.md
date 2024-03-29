[Go back](./../README.md)

## Contents
* [Node](./node/README.md)
* [Async try await catch - Funtion based](#async-try-await-catch---funtion-based)
* [Service Worker Code for PWA](#service-worker-code-for-pwa)
* [IndexedDB](#indexeddb)


---
### Promise
```javascript
/**
    * We can build promise ladder by return promise at end of .then function 
*/
const promise = new Promise((resolve,reject) => {
    if(promisedone) resolve(<solved param>);     // reached at .then 
    else    reject(<error parm>);                // reached at .catch
})
```
we can convert call backs to Promise by enclosing them in a new promise.


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
    // Contains the Cache Pages No need to include ICONS,SERVICE WORKER and MANIFEST FILE
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

---

### IndexedDB
Open a data leads to a request.
|Event|Description|
|:-|:-|
|`error`|Error in creating Database |
|`upgradeneeded`| When version changed,we need to update.We can only add the store to this only in this. |
|`success`| Data base created and we can use it |

[Source Tutorial](https://youtube.com/playlist?list=PLyuRouwmQCjmNyAysdqjNz5fIS5cYU4vi)

```javascript
let db = null;
const request = indexedDB.open('databasename', 1);

request.addEventListener('error', (err) => console.warn(err));
request.addEventListener('upgradeneeded', (event) => {
    db = event.target.result;
    if (!db.objectStoreNames.contains('storename')) db.createObjectStore('storename', {
        keyPath: 'store-key-field'
    })
})
request.addEventListener('success', (event) => {
    db = event.target.result;
})
```

`database.transaction(storename, 'readwrite').objectStore(storename);` this allows to excute the operations of database.

```javascript
/**
 * 
 * @param {IDBDatabase} database 
 * @param {String} storename - Valid Store Name
 * @param {Object} payload - ACTION,DATA,KEY
 * @returns {Promise}
 */
const excuteTransaction = (database, storename, payload) => new Promise((resolve, reject) => {
    const store = database.transaction(storename, 'readwrite').objectStore(storename);
    let request = null;
    switch (payload.ACTION) {
        case 'ADD':
            request = store.add(payload.DATA);
            break;
        case 'DELETE':
            request = store.delete(payload.KEY);
            break;
        case 'UPDATE':
            request = store.put(payload.KEY, payload.DATA);
            break;
        case 'GET':
            request = store.get(payload.KEY);
            break;
        case 'GETALL':
            request = store.getAll();
            break;
        default:
            onError('PAYLOAD ERROR');
            return;
    }
    request.onsuccess = (event) => resolve(event);
    request.onerror = (error) => reject(error);
});
```
