## Single Responsibility Principles (S.R.P)

A class should have only one reason to change.
```typescript title:single-responsability-violation.ts
Class EmailService{
	sendEmail(recipiant:string,subject:string,body:string):void{
		
	}
	
	loadEmailTemplate(templateName:string){
		
	}
	
	updateEmailTemplate(templateName:string,newContent:string){
	
	}
}
```

```typescript title:single-responsability.ts
class EmailSender{
	sendEmail(recipient:string,subject:string,body:string){
	
	}
}

class EmailTemplateManger{
	loadEmailTemplate(templateName:string){
	
	}
	
	updateEmailTemplate(templateName:string,newContent:string){
	
	}
}
```

---
## Open / Closed

Software entities (classes,modules,functions,etc) should be open for extention but closed for modification
```typescript title:open-close-violation.ts
class DiscountCalculator{
	calculateDiscount(product: Product): number {
	    switch (product.getType()) {
	      case "electronics":
	        return product.getPrice() * 0.1;
	      case "clothing":
	        return product.getPrice() * 0.2;
	      case "books":
	        return product.getPrice() * 0.4;
	      default:
	        return 0;
    }
  }
}
```

```typescript title:open-close.ts
interface DiscountStrategy{
	calculateDiscount(product:Product):number;
}

class ElectronicsDiscountStrategy implement DiscountStrategy{
	calculateDiscount(product:Product):number{
		return product.getPrice()*0.01;
	}
}

class BooksDiscountStrategy implement DiscountStrategy{
	calculateDiscount(product:Product):number{
		return product.getPrice()*0.02;
	}
}

class DiscountCalculator{
	private strategy :DiscountStrategy;
	
	constructor(strategy:DiscountStrategy){
		this.strategy = strategy;
	}
	
	calcDiscount(product:Product){
		return strategy.calculateDiscount(product);
	}
}
```

---
## Liskov Substitution 
if C is a subtype of P, then objects of type P may be replaced with objects of type C without altering any of the desirable properties of the program
```typescript title:liskov-violation.ts
	class Employee {

	readonly name: string;
	protected hoursWorked: number;
	
	constructor(name: string, hoursWorked: number) {
		this.name = name;
		this.hoursWorked = hoursWorked;
	}

	calculateSalary(): number {
		return this.hoursWorked * 10;
	}
}

  

class FullTimeEmployee extends Employee {

// Override the parent implementation

	override calculateSalary(): number {
	
	// maybe full-time employees get a fixed bonus
	
		return this.hoursWorked * 15 + 500;
	}
}

  

class PartTimeEmployee extends Employee{

	override calculateSalary():number{
	
		return this.hoursWorked *8;
	}
}
```

```typescript title:liskov.ts
class Employee {
    readonly name: string;
    protected hoursWorked: number;

    constructor(name: string, hoursWorked: number) {
        this.name = name;
        this.hoursWorked = hoursWorked;
    }

}

interface SalaryCalculator{
    calculateSalary():Number;
}

class FullTimeEmployee extends Employee implements SalaryCalculator {
    // Override the parent implementation
     calculateSalary(): number {
        // maybe full-time employees get a fixed bonus
        return this.hoursWorked * 15 + 500;
    }
}

class PartTimeEmployee extends Employee implements SalaryCalculator{
    calculateSalary():number{
        return this.hoursWorked *8;
    }
}
```
---
## Interface Segregation

```typescript title:interface-segregation-violation.ts

interface TaskManger{

	createTask(taskName:string):void;
	
	assignTask(taskName:string,assigne:string):void;
	
	sendNotification(message:string,recipient:string):void;
}

  

class TaskService implements TaskManger{

	createTask(taskName:string){
		console.log(taskName);
	}

  

	assignTask(taskName:string,assigne:string){
		console.log(taskName,assigne);
	}

	sendNotification(message:string,recipient:string){
		console.log(message,recipient);
	}

}
```

```typescript title:interface-segregation.ts
interface TaskManger{

createTask(taskName:string):void;

assignTask(taskName:string,assigne:string):void;

}

interface NotificationManger{

sendNotification(message:string,recipient:string):void;

}

  

class TaskService implements TaskManger{

createTask(taskName:string){

console.log(taskName);

}

  

assignTask(taskName:string,assigne:string){

console.log(taskName,assigne);

}

}
```
---
## Dependency Inversion

```typescript title:dependency-inversion-violation.ts
class OrderDataAccess{
	fetchOrders(){
	}
}

class OrderMangementService{
	private orderDataAccess:OrderDataAccess;
	
	BusinessLogic(){
		this.orderDataAccess=new OrderDataAccess();
	}
	
	doBusinessLogic(){
		orderDataAccess.getchOrders();
	}
}
```

```typescript title:dependency-inversion.ts
interface DataProvider{
	fetchData():void;
}

class OrderMySqlDataAccess implements DataProvider {
	fetchData():void{
	
	}
}

class OrderMongoDataAccess implements DataProvider {
	fetchData():void{
	
	}
}

class OrderMangementService {
	private dataProvider:DataProvider;
	
	constructor(dataProvider:DataProvider){
		this.dataProvider=dataProvider;
	}
	
	
	doBusinessLogic(){
		dataProvider.fetchData();
	}
}
```