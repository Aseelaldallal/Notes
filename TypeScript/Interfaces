# Interfaces


### Why Interfaces?

An interface is a contract signed by an object that guarantees that the object has certain properties and functions.

### Creating Interfaces

```javascript
function greet { person: {name: string}) {
	console.log("Hello " + person.name);
}

const person = {
	firstName: "Max", 
	age: 27
}

greet(person);
```

You get an error because you're saying

```javascript
function greet { person: {name: string})
```

and person does not have the field 'name'

The problem with the above approach is assume you have a function

```javascript
function changeName({person: {name: string}) {
	person.name = "Anna";
}
```

See the repetition? 

Better way, use Interface Keyword

```javascript
interface NamedPerson {
	firstName: string
}

function greet { person: NamedPerson ) {
	console.log("Hello " + person.name);
}

function changeName({person: NamedPerson) {
	person.name = "Anna";
}

const person = {
	firstName: "Max", 
	age: 27
}
```

If we change the code to 

```javascript
const person = {
	firstName: "Max", 
	age: 27
}
```

We'll get an error saying interface requirements not met.

Now, if you try

```greet({firstName: "Max", age: 27});```

Once you pass an object literal directly, typescript checks are more rigorous. In the above case, it will throw an error saying that age doesn't exist in NamedPerson.

Either you don't pass object literals directly OR make your interfaces very defined.

```
interface NamedPerson {
	firstName: string;
	age?: number
}
```

The ? indicates an optional argument. So you can go ahead and run 

```greet({firstName: "Max", age: 27});```

**What if you don't know the name of the properties in advance?**


```
interface NamedPerson {
	firstName: string;
	age?: number;
	[propName: string]: any // if you don't know the type
}
```

Now you can add anything to the person class, and it'll work

```javascript
const person = {
	firstName: "Max", 
	age: 27,
	hobbies: ["Cooking"]
}
```


### Methods on Interfaces

```
interface NamedPerson {
	firstName: string;
	age?: number;
	[propName: string]: any,
	greet(lastName: string) : void;
}
```

Now you have to implement the greet method.

```javascript
const person : NamePerson = {
	firstName: "Max", 
	age: 27,
	hobbies: ["Cooking"],
	greet(lastName: string) {
		console.log("Hi I am " + this.firstName);
	}
}

person.greet("Anything");

```

### Classes and Interfaces

```javascript
class Person implements NamedPerson {
	firstName: string;
	greet(lastName: string) {
		console.log("Hi I am " + this.firstName);
	}
}

const myPerson = new Person();
myPerson.firstName = "Aseel";
greet(myPerson); 
```

You can add more properties to your person class, as long as you implement what the interface requires.

### Interfaces and Function Types

```javascript
interface DoubleValueFunc {
	(number1: number, number2: number) : number;
}

Whatever uses this interface MUST be a function of this type.

let myDoubleFunction : DoubleValueFunc;
myDoubleFunction = function(val1: number, val2: number) {
	return (val1 + val2) * 2;
}

console.log(myDoubleFunction(10,20)); 
```

We're just creating an interface which says that the type should be a function which gets two arguments here both arguments are numbers, and returns a number.

### Interface Inheritance

```javascript
interface AgedPerson extends NamedPerson {
	age: number; // now its required, it was optional in NamedPerson
}

const oldPerson: AgedPerson = {
	age: 27,
	firstName: "Asel",
	greet(lastName: string) {
		console.log("Hello!");
	}
}
```

So oldPerson needs to have all the properties of AgedPerson and Person, and whatever is in AgedPerson supersedes what is in Person.

### How do Interfaces get compiled?

How does the interface code gets compiled into JavaScript? Interfaces don't get compiled to .js, they're just there to give you errors during compilation when working with TypeScript.


