## Types

### Functions


*** Specifying Function Return Type ***

In the example below, we are expecting the function to return a string.

```javascript
function returnMyName() : string {
  return myName;
}
```

*** Specifying Function Parameter Types ***

```javascript
function multiply(value1: number, value2: number) : number {
  return value1*value2;
}
```

*** Specifying Function Types ***

let myMultiply: (val1: number, val2: number) => number;

### Objects

```javascript
let userData = {
	name: "Max",
	age: 27
}
userData = {}
```

The code returns and error "The empty object is not assignable to type {name: string; age: number;}". Basically typescript infers the type of object 'userData' to be an object with a name field (type string) and an age field (of type number). 
The property names are important here. If we write

```javascript
userData = {
	a: "max",
	b: 27
}
```

We still get an error. 

*** Assigning Object Types ***

```javascript
let userData: { name: string, age: number } = {
	name: "max",
	age: 27
}
```

*** Complex Object ***

```javascript
let complex: { data: number[], output: (all: boolean) => number{}} = {
	data: [100,2,10],
	output: function (all: boolean) : number [] {
		return this.data;
	}
}
```

Basically we have an object with a data field which is an array of numbers, and output function which takes a single parameter 'all', a boolean', and returns a number.

Now lets say we have complex2, and we want it to be the same as complex. 

```javascript
let complex2: { data: number[], output: (all: boolean) => number{}} = {
	data: [100,2,10],
	output: function (all: boolean) : number [] {
		return this.data;
	}
}
```

Now what if we want data to be a mixed array, not just numbers. So we'd have to switch number[] to any[] in two places.

To solve this problem, we can create a type alias.

### Type Alias

```javascript
type Complex = {data: number[], output: (all: boolean) => number[]);
let complex2: Complex = {
	data: [100,2,10],
	output: function (all: boolean) : number [] {
		return this.data;
	}
}
```

Now we have a reusable type.

### Union Types

```javascript
let myRealAge : any = 27
myRealAge = "27";
```

This doesn't give an error. But what if we ONLY want this to be a number OR a string ONLY. We can do this

```javascript
let myRealAge: number | string = 27
myRealAge = true; // ERROR
``` 

### Checking Types

```javascript
if(typeof finalValue == "number") ... // put type between quotes
```

### Never Type

```javascript
function neverReturns() : never {
	throw new Error('An Error!')
}
```

This function is NEVER returning anything. Use this in parts of your code you know will never be reached.

### Non-Nullable Types

```javascript
let canBeNull = 12;
canBeNull = null;
let canAlsoBeNull; // type any since we didn't specify
canAlsoBeNull = null;
```

Issue: Lead to problems. Because you might have null in a place you want to use this number to do a calculation. 

tsconfig.js:
"strictNullChecks": true

Now, if you try to compile the code above, you get an error. But what if we want to allow null?

```
let canBeNull: number | null = 12
```

Now canBeNull is nullable.

```
let canThisBeAny = null;
canThisBeAny = 12;
```

Error: cannot assign number to type null.

Note: This is only useful is strictNullChecks are true.







