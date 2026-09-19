

### 1. What is a callback function?

A callback function is a function that is passed as an argument to another function,       
to be executed later, either after some work finishes or when some event occurs.      

---

### 2. What is callback hell?

Callback hell (also called the pyramid of doom) happens when many asynchronous operations depend on each other    
and are written as deeply nested callbacks. The code drifts to the right, becomes hard to read, and error handling gets repetitive.   

Problems: poor readability, difficult debugging.

Ways to avoid it:

- Use Promises and chain them with .then() .
- Use async / await to write async code that reads top to bottom.
- Break logic into small, named functions instead of anonymous nested ones.

---

### 3. How can we handle errors in promises?

There are two ways: .catch() or try and catch{} block.          

---

### 4. What is a promise?

A Promise is an object that represents the eventual completion (or failure) of an     
asynchronous operation and its resulting value.

---

### 5. What is the difference between Promise.any() and Promise.all()?

Both take an iterable of promises and return a single promise, but they have opposite goals.

Promise.all() waits for every promise to fulfill and then returns an array of all the results in input order.     
It fails, if any single promise rejects, the whole thing rejects immediately with that first rejection reason.     

Promise.any() only needs one success. It fulfills with the value of the first promise that fulfills,     
and it rejects only when all the promises reject, with an AggregateError that holds every reason.      



---

### 6. What is the filter() method?

filter() is an array method that creates a new array containing only the elements for which the callback function returns a truthy value.        
It does not modify the original array.



---

### 7. What is the map() function?

map() is an array method that creates a **new array** by calling a function on **every element** of the original array and    
collecting the returned values.The new array always has the same length as the original,    
and the original array is not modified.    


---

### 8. When do we use the finally block?

The finally block contains code that must run regardless of whether an operation succeeded or failed. It is mainly used for cleanup.      
---

### 9. How can we resolve multiple promises?

JavaScript provides static methods on `Promise` for working with several promises at once:

Promise.all() waits for all to fulfill, rejects immediately if any rejects
Promise.allSettled() waits for all to settle, never rejects, returns each outcome (`fulfilled` or `rejected`)

---

### 10. What is flatMap()?

flatMap() is an array method that maps each element using a callback and then flattens the result one level deep into a new array.     
It is equivalent to `map()` followed by `flat(1)`, but slightly more efficient.     

---

### 11. What is the difference between async and await ?

async and await are two keywords that work together. They are not alternatives to each other.

async-->
async Placed before a function to declare it as asynchronous. The function always returns a promise.       
A returned value is automatically wrapped in a resolved promise, and a thrown error becomes a rejected promise.


await-->
await Placed before a promise inside an async function (or at the top level of an ES module outside of async function).          
It pauses execution of that function until the promise settles, then returns the fulfilled value or throws the rejection reason.    

---

### 12. Why do we prefer async and await over promises?

async / await is built on top of promises. It is syntax that makes promise-based code easier      
to write and read. Reasons it is often preferred:

1. Readability: Asynchronous code looks like synchronous code, reads top to bottom, and avoids long `.then()` chains.
2. Simpler error handling: A single `try...catch` covers both synchronous and asynchronous errors.
3. Easier debugging: Stack traces are clearer, and you can step through `await` lines in a debugger like normal code.
4. Natural control flow: Loops, `if` statements and early returns work naturally, which is awkward inside promise chains.
5. Easier to share values: Variables from earlier steps stay in the same scope, with no need to pass data down a chain or nest `.then()` calls.

