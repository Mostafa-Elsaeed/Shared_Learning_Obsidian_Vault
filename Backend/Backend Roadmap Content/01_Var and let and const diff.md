[[Var, Let, and Const – What's the Difference]]

## Var:

- it's a global scope variable which you can access outside of it's local scope.

**Example:**

```
	var tester = "hey hi";
    function newFunction() {
        var hello = "hello";
    }
    console.log(hello); // error: hello is not defined
```

- var can be redeclared without throwing any errors
**Example:**

```
	var greeter = "hey hi";
    var times = 4;

    if (times > 3) {
        var greeter = "say Hello instead"; 
    }

    console.log(greeter) // "say Hello instead"
```

- var can be overridden
**Example:**

```
	var greeting = "say Hi";
    greeting = "say Hello instead";
```
## Let:
- is a block scope variable which can't be access outsode of it's local scope.
**Example:**

```
	 if (times > 3) {
	        let hello = "say Hello instead";
	        console.log(hello);// "say Hello instead"
	    }
   console.log(hello) // hello is not defined
```

- let can't be redeclared and if so it will throw an error
**Example:**

```
	let greeting = "say Hi";
    let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

- let can be overridden
**Example:**

```
	 let greeting = "say Hi";
    greeting = "say Hello instead";
```

## Const
- Const is a block scope variable which can't be access outsode of it's local scope.
**Example:**
```
	 if (times > 3) {
	        const hello = "say Hello instead";
	        console.log(hello);// "say Hello instead"
	    }
   console.log(hello) // hello is not defined
```

- const can't be redeclared and if so it will throw an error
**Example:**

```
	const greeting = "say Hi";
    const greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

- const can't be overridden
**Example:**

```
	 const greeting = "say Hi";
    greeting = "say Hello instead";
```