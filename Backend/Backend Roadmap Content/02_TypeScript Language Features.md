[[Learn Object-Oriented Programming in TypeScript]]

## Object:

Object: An object is a data type that stores a collection of values organized into key/value pairs

**Example:** 

```
const person = {
  name: "Lucas", // primitive value of type string
  surname: "Garcez",
  age: 28, // primitive value of type number
  address: {
    // object type containing the keys "city" and "country"
    city: "Melbourne",
    country: "Australia",
  },
};
```

## Class:

Class: is a **blueprint** for creating objects that have certain **properties** (data) and **methods** (functions).

**Example**

```
class Person {
  name: string; // attribute
  surname: string; // attribute
  age: number; // attribute

  // constructor method (special method)
  constructor(name: string, surname: string, age: number) {
    this.name = name;
    this.surname = surname;
    this.age = age;
  }

  // method to obtain the full name: "Lucas Garcez"
  getFullName() {
    return `${this.name} ${this.surname}`;
  }
}
```

- **Constructor Method:**
		The constructor is a special method within a class. It’s automatically invoked when a new object is created. Constructors are responsible for initializing the class attributes with values provided during object creation. In TypeScript, the constructor is defined using the **constructor** keyword, as you can see in the code above.
- **Instance:**
		An instance refers to an object created from a class.
		**Example:**
		```
		const lucas = new Person("Lucas", "Garcez", 28);
		lucas.name; // "Lucas"
		lucas.getFullName(); // "Lucas Garcez"
		```
- **Interface:**
		An interface defines a contract establishing which attributes and methods a class must implement.
		**Example:**
		```
		interface BankAccount {
		  balance: number;
		  deposit(amount: number): void;
		  withdraw(amount: number): void;
		}
		
		class CurrentAccount implements BankAccount {
		  balance: number;
		  // The class can have other attributes and methods
		  // beyond those specified in the interface
		  overdraftLimit: number;
		
		  deposit(amount: number): void {
		    this.balance += amount;
		  }
		
		  withdraw(amount: number): void {
		    if (amount <= this.balance) {
		      this.balance -= amount;
		    }
		  }
		}
		```
- **Abstract Class:**
		abstract classes define a model or contract that other classes must follow. But while an interface only describes the structure of a class without providing implementations, an abstract class can include method declarations and concrete implementations.
		**Example:**
		```
		abstract class BankAccount {
		  balance: number;
		
		  constructor(initialBalance: number) {
		    this.balance = initialBalance;
		  }
		
		  // Concrete method (with implementation)
		  deposit(amount: number): void {
		    this.balance += amount;
		  }
		
		  // Abstract method (must be implemented by subclasses)
		  abstract withdraw(amount: number): void;
		}
		
		class CurrentAccount extends BankAccount {
		  withdraw(amount: number): void {
		    const fee = 2; // Current accounts have a fixed withdrawal fee
		    const totalAmount = amount + fee;
		
		    if (this.balance >= totalAmount) {
		      this.balance -= totalAmount;
		    } else {
		      console.log("Insufficient balance.");
		    }
		  }
		}
		```