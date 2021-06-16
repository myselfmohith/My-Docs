###### NOTE: This contains ***my*** some tricks and shortcuts for Javascript
## Contents
* [Async try await catch - Funtion based](#async-try-await-catch---funtion-based)


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