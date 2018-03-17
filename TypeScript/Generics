# Generics

## Why and What are Generics?

**Simple Generic**

```javascript
function echo(data: any) {
    return data;
}

console.log(echo("Max"));
console.log(echo(27));
console.log(echo({age: 27});
```

This function is generic function because we have this any type. The big disadvantage with the any type is that you get back any data. 

Let's say you have

```console.log(echo(27).length);```

Now when you go to console, you'll get undefined because a number doesn't have a length. 

It would be nice if such function accepted any input, but was aware of the type of data it returns. I.e, we want the above line of code to give an error in compilation. 

Better Generic

```javascript
function betterEcho<T>(data: T) {
	return data;
}
```


This construct tells TypeScript that this is a generic function. 
Now, with <T> tells TypeScript when using this function give me
the type and then I'll be able to use it.

```
console.log(betterEcho("Max").length); // works
console.log(betterEcho(27).length); // fails
```

Second line gives number does not have property length on compilation.

You could also do something like this

```
console.log(betterEcho<number>(27)); // works
console.log(betterEcho<number>("27")); // fails
```

## Built in Generics

**Arrays**

const testResults = []

