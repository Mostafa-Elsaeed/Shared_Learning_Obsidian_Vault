### 1. Promise.all
- Takes an array (or iterable) of promises.
- Resolves **when all promises succeed**, returning an array of results (in the same order).
- Rejects immediately if **any promise fails**.
```typescript title:promise.all.ts
Promise.all([p1, p2, p3])
  .then(results => console.log(results)) // [res1, res2, res3]
  .catch(err => console.error(err)); // stops if one fails
```
---

### 2. Promise.allSettled
- Waits for **all promises to finish**, no matter if they resolve or reject.
- Always resolves with an array of objects showing the `status` and either `value` or `reason`.
```typescript title:promise.allsettled.ts
Promise.allSettled([p1, p2, p3])
  .then(results => console.log(results));
// [{status: "fulfilled", value: ...}, {status: "rejected", reason: ...}, ...]
```
---

### 3. **`Promise.race`**
- Resolves or rejects **as soon as the first promise settles** (whichever happens first).
- Useful for **timeouts or picking the fastest result**.
```typescript title:inheritance.ts
Promise.race([p1, p2, timeoutPromise])   .then(res => console.log(res)) // first one to resolve   .catch(err => console.error(err)); // or first reject
```

---

### 4. **`Promise.any`**
- Resolves as soon as **the first promise fulfills**.
- If **all promises reject**, it rejects with an `AggregateError`.
```typescript title:inheritance.ts
Promise.any([p1, p2, p3]).then(res => console.log(res)) 
// first successful result   
.catch(err => console.error(err.errors)); 
// all failed
```

---

### 5. **`Promise.resolve` & `Promise.reject`**
- Create a promise that is immediately resolved or rejected.
    
```typescript title:inheritance.ts
Promise.resolve(42).then(console.log); // 42
Promise.reject("Error").catch(console.error); // Error
```
