
Non-blocking
  - Task always blocked for the result
  - The thread is not blocked

Asynchronous === Scalability
  - Scalability will always impact performance within a reasonable cost boundary. Acheiving both costs a lot

Asynchronous Style 1
  - Callback
      function () {
        ...
        fetchData(input, callback)
        ...
      }
      Problem with this is no standards for callback, error handling from the called method and worse error handling during the calling of callback itself

function compute(n) {
  return new Promise(function(resolve, reject) {
    if (n<0) {
      reject ("invalid argument")
    } else {
      setTimeout(() => resolve(n*2), 1000)
    }
  }
}
Promises exist in one of 3 states: Pending, Resolve*, Rejected*
 *Terminal state

Promises use something called Railway Track Pattern

then, catch pattern makes it hard to track the flow of the program

Java 8 - Completable Future === Promises in JS

JS - non blocking
async function call(n) {
 try{   
    const result = await compute(2);
    const step2 = result + 1;
    const step3 = result * 10;
    
    const step4 = transform(step3)
    console.log('The result is ${step4}')
  }catch (ex) {
    console.log(ex)
  }
}

In Java, the same thing can be acheived using Virtual threads

By using Virtual threads you can acheive Scalability 

- In the past the structure of imperative style parallel code was very different from the structure of imperative style sequential  code.

- With parallel streams since Java 8, the structure of functional style parallel code is the same as the structure of the functional style sequential code.

- With CompletableFuture (similar to JS Promises), the structure of functional style asynchronous code is the same as the structure of funtional style synchronous code.

- The functional style code is great as long as we don;t have to deal with exceptions. With exception this quickly turns into a mess.

- With virtual threads(similar to async/await in JS), the structure of asynvhronous imperative style code is the same as the structure of synchrounous imperative style code.

