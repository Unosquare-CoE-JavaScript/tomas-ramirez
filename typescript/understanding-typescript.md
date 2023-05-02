# What is TypeScript

TypeScript is an open-source programming language that is a typed superset of JavaScript. It was developed
to help JS developers to write more robust and maintainable JavaScript code.
TypeScript adds static type-checking to JavaScript, which means that the language will catch errors during development,
rather than at runtime.

Some basic types in TypeScript:

- number: integers and floating-point numbers.
- string: a sequence of characters.
- boolean: true or false.
- null and undefined: represent the absence of a value.
- any: represents any type of value. This is the default type in JavaScript and can be used to opt-out of type checking.
- void: represents the absence of a value. This is typically used as the return type of functions that don't return
  anything.
- never: represents a value that can never be reached. This is typically used as the return type of functions that
  always throw an error or enter an infinite loop.
- arrays: The array type represents a collection of values of a specific type.
- tuples: The tuple type represents an array with a fixed number of elements, where each element may have a different
  type.
- Enum: The enum type is used to give friendly names to a set of numeric values.
- Object Types: Type aliases can be used to "create" your own types. You're not limited to storing union types though -
  you can also provide an alias to a (possibly complex) object type.

```typescript
const num: number = 42;
const str: string = "hello";
const bool: boolean = true;
const nul: null = null;
const undef: undefined = undefined;
const anyVal: any = "some value";
const voidVal: void = undefined;
const neverVal: never = (() => {
    throw new Error("never")
})();
let list: number[] = [1, 2, 3];
let fruits: Array<string> = ['apple', 'banana', 'orange'];
let x: [string, number];
x = ['hello', 10];

enum Color {
    Red,
    Green,
    Blue,
}

let red: Color = Color.Red;

type User = { name: string; age: number };
const u1: User = {name: 'Max', age: 30};
```

## Type Casing

In TypeScript, you work with types like string or number all the times.
Important: It is string and number (etc.), NOT String, Number etc.
The core primitive types in TypeScript are all lowercase!

## TypeScript Functions as Types

In TypeScript, functions can be defined as types, which can be used to describe the shape of a function or to specify
the type of a variable that holds a function.

### Defining Function Types

To define a function type, we use the following syntax:

makefile

```typescript
(parameter1: type1, parameter2: type2, ...) => returnType
```

``` typescript
type AddFunction = (a: number, b: number) => number;
```

### Using Function Types

Once we've defined a function type, we can use it to specify the type of a variable or parameter that holds a function.

### Optional and Default Parameters

Function types can also include optional and default parameters. To specify an optional parameter, we use a question
mark ? after the parameter name, and for default parameters we use the = followed by the default value like this:

``` typescript
type GreetingFunction = (name?: string, discount: number = 0) => string;
```

### Interfaces

Interfaces allow you to define the shape of an object or class, including its properties and methods.

```typescript
interface Person {
    name: string;
    age: number;

    greet(): void;
}

class Tom implements Person {
    name = "Tom";
    age = 30;

    greet() {
        console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
    }
}
```

### Type Annotations

Type annotations allow you to specify the type of a variable, parameter, or property.

```typescript
function sum(a: number, b: number): number {
    return a + b;
}

class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}
```

### Generics

Generics allow you to write reusable code that works with a variety of types.

```typescript
function genericDuh<T>(value: T): T {
    return value;
}

const num = genericDuh(42);
const str = genericDuh("Hello, world!");
```

### Decorators

Decorators are a way to add annotations or metadata to classes, methods, and properties at design time.
Decorators are a form of metaprogramming that allow you to modify the behavior of a class or its members without
changing the original code.

### Defining Decorators

Decorators are defined using the @ symbol followed by a function that is executed at design time. The decorator function
takes one or more arguments that represent the target of the decorator.

```typescript
function logClass(target: any) {
    console.log(`Class ${target.name} was decorated.`);
}

@logClass
class MyClass {
}
```

### Applying Decorators

Decorators can be applied to classes, methods, and properties. When a decorator is applied, it modifies the behavior of
the target in some way.

```typescript
function prefixMethod(prefix: string) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        const originalMethod = descriptor.value;
        descriptor.value = function (...args: any[]) {
            console.log(`Calling method ${prefix}${propertyKey}.`);
            return originalMethod.apply(this, args);
        }
        return descriptor;
    }
}

class MyClass {
    @prefixMethod("customPrefix_")
    myMethod() {
    }
}
```

- we've defined a decorator function called prefixMethod that returns another function that modifies the descriptor
  of the decorated method.
- The modified method logs a message before calling the original method.
- We've applied this decorator to the myMethod method of the MyClass class using the @ symbol.

### Built-in Decorators

TypeScript also provides a number of built-in decorators that you can use to modify the behavior of classes and their
members.

- @deprecated: Marks a class or member as deprecated and logs a warning when it is used.
- @sealed: Prevents the addition of new properties to a class or object.
- @freeze: Freezes the properties of a class or object, preventing them from being modified.
- @abstract: Marks a class or method as abstract, which requires derived classes to implement the method.

### Limitations of Decorators

- Decorators can only be used at design time, not at runtime.
- Decorators cannot modify the behavior of built-in JavaScript objects or methods.
- Decorators can only modify the behavior of the target class or its members, not the behavior of external code that
  uses the class.

## TypeScript Advanced Types

TypeScript provides a number of advanced type features that can help you write more expressive and safer code. These
features include union types, intersection types, type guards, and more.

### Union Types

A union type allows a variable to have multiple types. This is useful when you need to work with values that can be of
different types.

```typescript
let myVar: string | number;
```

myVar can be either a string or a number. We can assign a value to myVar of either type:

```typescript
myVar = "hello";
myVar = 42;
```

We can also use conditional statements and type guards to check the type of myVar at runtime:

```javascript
if (typeof myVar === "string") {
    console.log("myVar is a string.");
} else if (typeof myVar === "number") {
    console.log("myVar is a number.");
}
```

### Intersection Types

An intersection type combines multiple types into a single type that has every property of each type.

```typescript
type Car = {
    make: string;
    model: string;
    year: number;
};

type Truck = {
    make: string;
    model: string;
    year: number;
    capacity: number;
};
```

Both Car and Truck have the same properties, but Truck has an additional capacity property. We can use an
intersection type to create a new type that has all the properties of both:

```typescript
type CarAndTruck = Car & Truck;
```

Now, CarAndTruck has all the properties of Car and Truck:

```typescript
let myCarAndTruck: CarAndTruck = {
    make: "Mitsubishi",
    model: "Montero ",
    year: 1986,
    capacity: 11
};
```

### Type Guards

A type guard is a function that checks the type of a variable at runtime and returns a boolean value that indicates
whether the variable is of a certain type. This can be useful when working with union types.

```typescript
function isString(value: unknown): value is string {
    return typeof value === "string";
}
```

isString is a type guard function that checks whether value is a string.

TypeScript Modules & Namespaces
TypeScript provides two ways to organize code into reusable units: modules and namespaces.

## Modules

Modules allow you to encapsulate code into separate files. A module can export functions, classes, or other values that
can be imported by other modules.

To create a module in TypeScript, you can use the export keyword to export values from a file:

```typescript
export function sayHello(name: string) {
    console.log(`Hello, ${name}!`);
}
```

You can then import this function in another module using the import keyword:

```typescript
import {sayHello} from './greeter';

sayHello('Tom');
```

You can also export classes, interfaces, and other types from a module:

```typescript
export interface Person {
    name: string;
    age: number;
}


export class Employee {
    constructor(public name: string, public salary: number) {
    }
}
```

## Namespaces

Namespaces allow you to group related code together into a single namespace. A namespace can contain functions, classes,
or other values, and can be used to prevent naming conflicts.

To create a namespace in TypeScript, you can use the namespace keyword:

typescript

```typescript
namespace MyNamespace {
    export function sayHello(name: string) {
        console.log(`Hello, ${name}!`);
    }
}
```

You can then access the functions in the namespace using the namespace name:

```typescript
MyNamespace.sayHello('Tom');
```

In this example, we call the sayHello function in the MyNamespace namespace with the argument 'Tom'.

Note that when using namespaces, you need to make sure to include all the necessary files in your application. If you're
using modules, this will be handled by TypeScript automatically.

## Next-Gen JavaScript

Next-Gen JavaScript includes new features that were introduced in recent versions of the language
By using these modern features, we write more powerful, maintainable, and efficient code.

## Arrow Functions

Arrow functions are a shorthand way to define functions using the => syntax.

```js
const sum = (a, b) => a + b;
``` 

## Template Literals

Template literals allow you to include variables and expressions inside a string using backticks.

```js
const name = "Tom";
console.log(`Hello, ${name}!`);
``` 

## Destructuring

Destructuring allows you to extract values from arrays and objects into variables.

```js
const numbers = [1, 2, 3];
const [a, b, c] = numbers;

const person = {name: "Tom", age: 25};
const {name, age} = person;
``` 

## Spread Operator

The spread operator allows you to spread an array into individual elements, or an object into individual properties.

```js
const numbers = [1, 2, 3];
console.log(...numbers);

const person = {name: "Tom", age: 25};
console.log({...person});
``` 

## Classes

Classes are a new way to define objects in JavaScript, with support for OOP terms such as inheritance and encapsulation.

```js
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
    }
}

const Tom = new Person("Tom", 25);
Tom.greet();
```
