## Asynchronous Programming

asynchronous actions - actions that we initiate now, but they finish later. Ex: setTimeout, loading scripts and modules

“callback-based” style of asynchronous programming - provide callback function that executes when the async action is complete.

“error-first callback” style - calls callback(null, script) for successful load and callback(error) otherwise.

“callback hell” or “pyramid of doom.” - when there are nested async functions to be performed one after another , callbacks grow. Solution to that is Promise.

```javascript
  loadScript('/my/script.js', function(error, script) {
    if (error) {
      // handle error
    } else {
      // script loaded successfully
    }
  });
```
## Promise
A promise is a special JavaScript object that links the “producing code” and the “consuming code” together. The constructor syntax for a promise object is:
```javascript
  let promise = new Promise(function(resolve, reject) {
    // the function is executed automatically when the promise is constructed
    // after 1 second signal that the job is done with the result "done"
    setTimeout(() => resolve ("done"), 1000); //Executor is called automatically and immediately by new Promise()
  });
```
The function passed to new Promise is called the executor. When new Promise is created, the executor runs automatically. Its arguments resolve and reject are callbacks provided by JavaScript itself. Our code is only inside the executor. When the executor obtains the result, be it soon or late, doesn’t matter, it should call one of these callbacks:

1. resolve(value) — if the job is finished successfully, with result value.
2. reject(error) — if an error has occurred, error is the error object.

So to summarize: the executor runs automatically and attempts to perform a job. When it is finished with the attempt, it calls resolve if it was successful or reject if there was an error.
The promise object returned by the new Promise constructor has these internal properties:
1. state — initially "pending", then changes to either "fulfilled" when resolve is called or "rejected" when reject is called.
2. result — initially undefined, then changes to value when resolve(value) is called or error when reject(error) is called.

To summarize, the executor should perform a job (usually something that takes time) and then call resolve or reject to change the state of the corresponding promise object. A promise that is either resolved or rejected is called “settled”. The executor should call only one resolve or one reject. Any state change is final. All further calls of resolve and reject are ignored. There can be only a single result or an error. Also, resolve/ reject expect only one argument (or none) and will ignore additional arguments. We also can call resolve or reject immediately
```javascript
    let promise = new Promise(function(resolve, reject) {
      resolve("done");
      reject(new Error("…")); // ignored
      setTimeout(() => resolve("…")); // ignored
    });
```

**Consumers: then, catch**
The properties state and result of the Promise object are internal. We can’t directly access them. We can use the methods .then/ .catch/ .finally for that. A Promise object serves as a link between the executor (the “producing code” or “singer”) and the consuming functions (the “fans”), which will receive the result or error. Consuming functions can be registered (subscribed) using the methods .then and .catch. 
The first argument of .then is a function that runs when the promise is resolved and receives the result. The second argument of .then is a function that runs when the promise is rejected and receives the error.
```javascript
  promise.then(
    function(result) { /* handle a successful result */ },
    function(error) { /* handle an error */ }
  );

  let promise = new Promise(function(resolve, reject) {
      setTimeout(() => resolve("done!"), 1000);
    });
  // resolve runs the first function in .then
  promise.then(
      result => alert(result), // shows "done!" after 1 second
      error => alert(error) // doesn't run. Runs when promise is rejected.
  )
  .finally(() => stop loading indicator)
  // If we’re interested only in successful completions, then we can provide only one function argument to .then:
  promise.then(alert); // shows "done!" after 1 second
  // If we’re interested only in errors, then we can use null as the first argument: .then(null, errorHandlingFunction).
  // Or we can use .catch(errorHandlingFunction), which is exactly the same:
  // .catch(f) is the same as promise.then(null, f)
  promise.catch(alert); // shows "Error: Whoops!" after 1 second
```

**Cleanup: finally**
Always runs when the promise is settled: be it resolve or reject. The idea of finally is to set up a handler for performing cleanup/finalizing after the previous operations are complete. E.g. stopping loading indicators, closing no longer needed connections, etc.
1. A finally handler has no arguments. In finally we don’t know whether the promise is successful or not. That’s all right, as our task is usually to perform “general” finalizing procedures. The promise outcome is handled by the next handler. It doesn’t get the outcome of the previous handler (it has no arguments). This outcome is passed through instead, to the next suitable handler.
2. A finally handler “passes through” the result or error to the next suitable handler. Can come before or after then, catch. If it comes before, moves to next suitable handler. If it comes after, just executes the finally. When finally throws an error, then the execution goes to the nearest error handler.
3. A finally handler also shouldn’t return anything. If it does, the returned value is silently ignored. The only exception to this rule is when a finally handler throws an error. Then this error goes to the next handler, instead of any previous outcome.

Promises are more flexible. We can add handlers any time: if the result is already there, they just execute.
**Promises vs Callbacks**
Promises                                                               
1. Promises allow us to do things in the natural order. First, we run loadScript(script) , and .then we write what to do with the result.
2. We can call .then on a Promise as many times as we want. Each time, we’re adding a new “fan”, a new subscribing function, to the “subscription list” - Promise Chaining

Callbacks
1. We must have a callback function at our disposal when calling loadScript(script, callback) . In other words, we must know what to do with the result before loadScript is called.
2. There can be only one callback.

## Promise Chaining
When we have sequence of asynchronous tasks to be performed one after another we can chain then using Promises. 
The idea is that the result is passed through the chain of .then handlers.
Here the flow is:
1. The initial promise resolves in 1 second (*),
2. Then the .then handler is called (**), which in turn creates a new promise (resolved with 2 value).
3. The next then (***) gets the result of the previous one, processes it (doubles) and passes it to the next handler.
4. …and so on.

The whole thing works, because every **call to a .then returns a new promise**, so that we can call the next .then on it. When a handler returns a value, it becomes the result of that promise, so the next .then is called with it.

A classic newbie error: technically we can also add many .then to a single promise. This is not chaining.
```javascript
  new Promise(function(resolve, reject) {
      setTimeout(() => resolve(1), 1000); // (*)
    }).then(function(script1) { // (**)
      alert(result); // 1
      return result * 2;
    }).then(function(script2) { // (***)
     return new Promise((resolve, reject) => { // A handler, used in .then(handler) may create and return a promise.
      // In that case further handlers wait until it settles, and then get its result.
      setTimeout(() => resolve(result * 2), 1000); // the most nested callback has access to all variables script1, script2
    });
  })

  // Not promise chaining
  // What we did here is just adding several handlers to one promise. They don’t pass the result to each other; instead they process it independently
  let promise = new Promise(function(resolve, reject) {
    setTimeout(() => resolve(1), 1000);
  });
  promise.then(function(result) {
    alert(result); // 1
    return result * 2;
  });
  promise.then(function(result) {
    alert(result); // 1
    return result * 2;
  });
```

**Thenables**
A handler may return not exactly a promise, but a so-called “thenable” object – an arbitrary object that has a method .then. It will be treated the same way as a promise. The idea is that 3rd-party libraries may implement “promise-compatible” objects of their own. They can have an extended set of methods, but also be compatible with native promises, because they implement .then.
```javascript
  class Thenable {
    constructor(num) {
      this.num = num;
    }
    then(resolve, reject) {
      alert(resolve); // function() { native code }
      // resolve with this.num*2 after the 1 second
      setTimeout(() => resolve(this.num * 2), 1000); // (**)
      }
    }
    new Promise(resolve => resolve(1))
      .then(result => {
      return new Thenable(result); // (*)
      })
    .then(alert); // shows 2 after 1000ms
```

**fetch** - makes network request and returns a promise. The promise resolves with a response object when the remote server responds with headers. To read the full response, we should call the method response.text()/response.json(): it returns a promise that resolves when the full text is downloaded from the remote server, with that text as a result.
```javascript
  // same as above, but response.json() parses the remote content as JSON
  fetch('/article/promise-chaining/user.json')
    .then(response => response.json())
    .then(user => alert(user.name)); // iliakan, got user name
```

## Error handling with promises
Promise chains are great at error handling. When a promise rejects, the control jumps to the closest rejection handler. The easiest way to catch all errors is to append .catch to the end of chain. This catches promise rejection and any errors thrown in then handlers.
```javascript
  // the execution: catch -> then
  new Promise((resolve, reject) => {
    throw new Error("Whoops!");
  }).catch(function(error) {
    alert("The error is handled, continue normally");
  }).then(() => alert("Next successful handler runs")); // Here the .catch block finishes normally. So the next successful .then handler is called.
```
.then also catches errors in the same manner as catch, if given the second argument (which is the error handler).

What happens when a regular error occurs and is not caught by try..catch? The script dies with a message in the console. A similar thing happens with unhandled promise rejections. The JavaScript engine tracks such rejections and generates a global error in that case. In the browser we can catch such errors using the event unhandledrejection:
```javascript
  window.addEventListener('unhandledrejection', function(event) {
    // the event object has two special properties:
    alert(event.promise); // [object Promise] - the promise that generated the error
    alert(event.reason); // Error: Whoops! - the unhandled error object
  });
  new Promise(function() {
    throw new Error("Whoops!");
  }); // no catch to handle the error
```


```javascript
```


