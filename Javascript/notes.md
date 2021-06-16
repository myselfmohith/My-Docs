###### NOTE: This contains ***my*** some tricks and shortcuts for Javascript

### Async try await catch - Funtion based
This allows me to avoid the callback functions and work as single **Function.**

```javascript
// @params -> promise
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