### 1. Promise.all
- Takes an array (or iterable) of promises.
- Resolves **when all promises succeed**, returning an array of results (in the same order).
- Rejects immediately if **any promise fails**.
```typescript title:promise.all.ts
Promise.all([p1, p2, p3])
  .then(results => console.log(results)) // [res1, res2, res3]
  .catch(err => console.error(err)); // stops if one fails
```
### 2. Promise.allSettled
- Waits for **all promises to finish**, no matter if they resolve or reject.
- Always resolves with an array of objects showing the `status` and either `value` or `reason`.
```
Promise.allSettled([p1, p2, p3])
  .then(results => console.log(results));
// [{status: "fulfilled", value: ...}, {status: "rejected", reason: ...}, ...]
```