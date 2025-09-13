[[Learn Object-Oriented Programming in TypeScript]]

## **Inheritance:**
Inheritance is a mechanism that allows a class to derive characteristics from another class. When a class `B` inherits from a class `A`, it means that `B` automatically acquires the attributes and methods of `A` without needing to redefine them.
**Example:**
```typescript title:inheritance.ts
// BankAccount is now a regular class where you define attributes and methods
// that will be reused by the child class CurrentAccount
class BankAccount {
  balance: number = 0;

  constructor(initialBalance: number) {
    this.balance = initialBalance;
  }

  deposit(amount: number): void {
    this.balance += amount;
  }

  withdraw(amount: number): void {
    if (amount <= this.balance) {
      this.balance -= amount;
    }
  }
}

// CurrentAccount is a subclass of BankAccount, meaning 
// it inherits its attributes and methods.
class CurrentAccount extends BankAccount {
  overdraftLimit: number; // new attribute exclusive to CurrentAccount

  // When specifying a constructor method for a subclass,
  // we need to call another special method, "super".
  // This method calls the superclass (BankAccount) constructor to ensure
  // it is initialized before creating the CurrentAccount object itself.
  constructor(initialBalance: number, overdraftLimit: number) {
    super(initialBalance); // Must match the superclass constructor method signature
    this.overdraftLimit = overdraftLimit;
  }

  // Even though the withdraw method already exists in the superclass (BankAccount),
  // it is overridden here. This means every time a CurrentAccount
  // object calls the withdraw method, this implementation will be used, 
  // ignoring the superclass method.
  override withdraw(amount: number): void {
    const totalAvailable = this.balance + this.overdraftLimit;
    if (amount > 0 && amount <= totalAvailable) {
      this.balance -= amount;
    }
  }
}

// Creating a CurrentAccount with an initial balance of $0.00
// and an overdraft limit of $100.
const currentAccount = new CurrentAccount(0, 100);

// Making a $200 deposit by calling the deposit method
// In this case, the method from BankAccount will be invoked
// since deposit was not overridden in CurrentAccount
currentAccount.deposit(200); // balance: 200

// Withdrawing $250 by calling the withdraw method
// In this case, the method from CurrentAccount will be invoked
// as it has been overridden in its definition
currentAccount.withdraw(250); // balance: -50
```

## Polymorphism

**Example:**
```typescript title:polymarphism.ts

class Player{

	constructor(public name:string){}

	attack():void{
		console.log('attacking now');
	}

}

  
  

class Amazon extends Player{

	constructor(name:string,public spears:number){
		super(name);
	}

	override attack():void{
		super.attack()
		console.log('attacking with spears');
		this.spears -=1;
	}

}

  

class Barbarian extends Player{

	constructor(name:string,public axeHealth:number){
		super(name);
	}

  
	override attack():void{
		super.attack()
		console.log('attacking with axe');
		this.axeHealth -=1;
	}

}

  

const amazonPlayer= new Amazon('walas',100);

  

amazonPlayer.attack();

  
  
  

const barbarianPlayer= new Barbarian('walas',100);

  

barbarianPlayer.attack();
```
## Encapsulation
Encapsulation is one of the fundamental principles of OOP, but its concept can be applied to any programming paradigm. It involves hiding the internal implementation details of a module, class, function, or any other software component, exposing only what is necessary for external use. This improves code security, maintainability, and modularity by preventing unauthorized access and ensuring controlled interactions.

**Example:**
```typescript title:encapsulation.ts
export class Person {
  private firstName: string; // Accessible only within the class itself
  private lastName: string; // Accessible only within the class itself
  protected birthDate: Date; // Accessible by subclasses but not from outside

  constructor(firstName: string, lastName: string, birthDate: Date) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.birthDate = birthDate;
  }

  // Public method that can be accessed from anywhere
  public getFullName(): string {
    return `${this.firstName} ${this.lastName}`;
  }
}

// The Professor class inherits from Person and can access
// attributes and methods according to their access modifiers.
class Professor extends Person {
  constructor(firstName: string, lastName: string, birthDate: Date) {
    super(firstName, lastName, birthDate); // Calls the superclass (Person) constructor
  }

  getProfile() {
    this.birthDate; // ✅ Accessible because it is protected
    this.getFullName(); // ✅ Accessible because it is public
    this.firstName; // ❌ Error! Cannot be accessed because it is private in the Person class
    this.lastName; // ❌ Error! Cannot be accessed because it is private in the Person class
  }
}

function main() {
  // Creating an instance of Professor
  const lucas = new Professor("Lucas", "Garcez", new Date("1996-02-06"));

  // Testing direct access to attributes and methods
  lucas.birthDate; // ❌ Error! birthDate is protected and can only be accessed within the class or subclasses
  lucas.getFullName(); // ✅ Accessible because it is a public method
  lucas.firstName; // ❌ Error! firstName is private and cannot be accessed outside the Person class
  lucas.lastName; // ❌ Error! lastName is also private and inaccessible outside the Person class
}
```
#### **Access Modifiers Table**

| **Modifier** | **Access within the class** | **Access in subclass** | **Access outside the class** |
| ------------ | --------------------------- | ---------------------- | ---------------------------- |
| `public`     | ✅ Yes                       | ✅ Yes                  | ✅ Yes                        |
| `protected`  | ✅ Yes                       | ✅ Yes                  | ❌ No                         |
| `private`    | ✅ Yes                       | ❌ No                   | ❌ No                         |
## Abstraction
is a contract that maybe have some implementation and may not and be implemented in the sub class
**Example:**
``` typescript title:abstraction.ts
interface BankAccountInterface {
  balance: number;
  deposit(amount: number): void;
  withdraw(amount: number): void;
}

// Abstraction using class
abstract class BankAccountClass {
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
```
