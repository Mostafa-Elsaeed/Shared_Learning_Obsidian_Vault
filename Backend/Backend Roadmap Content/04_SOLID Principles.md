## Single Responsibility Principles (S.R.P)
This principle states that every method/class should handle a single responsibility. This is important because it results in better readability of code and separation of concerns.
```typescript title:single-responsability.ts

const fetchPosts = async (userId: number) => {
  try {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}/posts`
    );
    return await response.json();
  } catch (e) {
    handleError(e, "Error while fetching Posts!");
  }
};
```
---
## Open / Closed

The core meaning of the Open/Closed principle is made clear by the statement: 
*open to extension, closed for modification.*
The idea is that a class, once implemented, should be closed for any further modification. If any more functionality is needed, it can be added later using extension features such as **inheritance**. This is primarily done to avoid breaking existing code and unit tests. It also results in a modular code.

## Liskov Substitution 
if C is a subtype of P, then objects of type P may be replaced with objects of type C without altering any of the desirable properties of the program
![[CleanShot 2025-08-27 at 15.41.38.png]]

![[CleanShot 2025-08-27 at 15.42.42.png]]
## Interface Segregation

## Dependency Inversion
