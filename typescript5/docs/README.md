<p align="center">
  <a href="https://www.typescriptlang.org" target="blank"><img style="border-radius: 10px;" src="../../doc-images/typescript-logo.png" width="80" alt="TypeScript Logo" /></a>
</p>

<h1 align="center">Learn TypeScript</h1>

<p align="center">
  <b>TypeScript</b> is a strongly typed programming language that builds on <b>JavaScript</b>, giving you better tooling at any scale.
</p>

## Contents

1. [TypeScript Introduction](./typescript-introduction.md)
2. [TypeScript Getting Started](./typescript-get-started.md)
3. [TypeScript Simple Types](./typescript-simple-types.md)
4. [TypeScript Special Types](./typescript-special-types.md)
5. [TypeScript Arrays](./typescript-arrays.md)
6. [TypeScript Tuples](./typescript-tuples.md)
7. [TypeScript Object Types](./typescript-object-types.md)
8. [TypeScript Enums](./typescript-enums.md)
9. [TypeScript Type Aliases and Interfaces](#)
10. [TypeScript Union Types](#)
11. [TypeScript Functions](#)
12. [TypeScript Casting](#)
13. [TypeScript Classes](#)
14. [TypeScript Basic Generics](#)
15. [TypeScript Utility Types](#)
16. [TypeScript Keyof](#)
17. [TypeScript Null & Undefined](#)
18. [TypeScript Definitely Typed](#)
19. [TypeScript 5.x Updates](#)

### 📜 References

- [W3Schools](https://www.w3schools.com/typescript)

- [TypeScript Documentation](https://www.typescriptlang.org/docs)

### 🤝 Contributors

- Mengsreang-Chhoeung [@mengsreang_dev](https://twitter.com/mengsreang_dev)

## TypeScript Type Aliases and Interfaces

TypeScript allows types to be defined separately from the variables that use them.

Aliases and Interfaces allows types to be easily shared between different variables/objects.

### Type Aliases

Type Aliases allow defining types with a custom name (an Alias).

Type Aliases can be used for primitives like `string` or more complex types such as `objects` and `arrays`:

```ts
type CarYear = number;
type CarType = string;
type CarModel = string;
type Car = {
  year: CarYear;
  type: CarType;
  model: CarModel;
};

const carYear: CarYear = 2001;
const carType: CarType = 'Toyota';
const carModel: CarModel = 'Corolla';
const car: Car = {
  year: carYear,
  type: carType,
  model: carModel,
};
```

### Interfaces

Interfaces are similar to type aliases, except they **only** apply to `object` types.

```ts
interface Rectangle {
  height: number;
  width: number;
}

const rectangle: Rectangle = {
  height: 20,
  width: 10,
};
```

### Extending Interfaces

Interfaces can extend each other's definition.

> **Extending** an interface means you are creating a new interface with the same properties as the original, plus something new.

```ts
interface Rectangle {
  height: number;
  width: number;
}

interface ColoredRectangle extends Rectangle {
  color: string;
}

const coloredRectangle: ColoredRectangle = {
  height: 20,
  width: 10,
  color: 'red',
};
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Union Types

**Union types** are used when a value can be more than a single type.

Such as when a property would be `string` or `number`.

### Union | (OR)

Using the `|` we are saying our parameter is a `string` or `number`:

```ts
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code}.`);
}
printStatusCode(404);
printStatusCode('404');
```

### Union Type Errors

**Note:** you need to know what your type is when union types are being used to avoid type errors:

```ts
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code.toUpperCase()}.`); // error: Property 'toUpperCase' does not exist ontype 'string | number'.
}
```

In our example we are having an issue invoking `toUpperCase()` as its a `string` method and `number` doesn't have access to it.

[🔼 Back to top](#typescript-tutorial)

## TypeScript Functions

TypeScript has a specific syntax for typing function parameters and return values.

Read more about functions [here](https://www.w3schools.com/js/js_functions.asp).

### Return Type

The type of the value returned by the function can be explicitly defined.

```ts
// the `: number` here specifies that this function returns a number
function getTime(): number {
  return new Date().getTime();
}
```

> If no return type is defined, TypeScript will attempt to infer it through the types of the variables or expressions returned.

### Void Return Type

The type `void` can be used to indicate a function doesn't return any value.

```ts
function printHello(): void {
  console.log('Hello!');
}
```

### Parameters

Function parameters are typed with a similar syntax as variable declarations.

```ts
function multiply(a: number, b: number) {
  return a * b;
}
```

> If no parameter type is defined, TypeScript will default to using any, unless additional type information is available as shown in the Default Parameters and Type Alias sections below.

### Optional Parameters

By default TypeScript will assume all parameters are required, but they can be explicitly marked as optional.

```ts
// the `?` operator here marks parameter `c` as optional
function add(a: number, b: number, c?: number) {
  return a + b + (c || 0);
}
```

### Default Parameters

For parameters with default values, the default value goes after the type annotation:

```ts
function pow(value: number, exponent: number = 10) {
  return value ** exponent;
}
```

TypeScript can also infer the type from the default value.

### Named Parameters

Typing named parameters follows the same pattern as typing normal parameters.

```ts
function divide({ dividend, divisor }: { dividend: number; divisor: number }) {
  return dividend / divisor;
}
```

### Rest Parameters

Rest parameters can be typed like normal parameters, but the type must be an array as rest parameters are always arrays.

```ts
function add(a: number, b: number, ...rest: number[]) {
  return a + b + rest.reduce((p, c) => p + c, 0);
}
```

### Type Alias

Function types can be specified separately from functions with type aliases.

These types are written similarly to arrow functions, read more about arrow functions [here](https://www.w3schools.com/js/js_arrow_function.asp).

```ts
type Negate = (value: number) => number;

// in this function, the parameter `value` automatically gets assigned the type `number` from the type `Negate`
const negateFunction: Negate = (value) => value * -1;
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Casting

There are times when working with types where it's necessary to override the type of a variable, such as when incorrect types are provided by a library.

Casting is the process of overriding a type.

### Casting with `as`

A straightforward way to cast a variable is using the `as` keyword, which will directly change the type of the given variable.

```ts
let x: unknown = 'hello';
console.log((x as string).length);
```

Casting doesn't actually change the type of the data within the variable, for example the following code will not work as expected since the variable `x` is still holds a number.

```ts
let x: unknown = 4;
console.log((x as string).length); // prints undefined since numbers don't have a length
```

TypeScript will still attempt to typecheck casts to prevent casts that don't seem correct, for example the following will throw a type error since TypeScript knows casting a string to a number doesn't makes sense without converting the data:

```ts
console.log((4 as string).length); // Error: Conversion of type 'number' to type 'string' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression to 'unknown' first.
```

The Force casting section below covers how to override this.

### Casting with `<>`

Using <> works the same as casting with `as`.

```ts
let x: unknown = 'hello';
console.log((<string>x).length);
```

> This type of casting will not work with TSX, such as when working on React files.

### Force casting

To override type errors that TypeScript may throw when casting, first cast to `unknown`, then to the target type.

```ts
let x = 'hello';
console.log((x as unknown as number).length); // x is not actually a number so this will return undefined
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Classes

TypeScript adds types and visibility modifiers to JavaScript classes.

Learn more about JavaScript classes [here](https://www.w3schools.com/js/js_classes.asp).

### Members: Types

The members of a class (properties & methods) are typed using type annotations, similar to variables.

```ts
class Person {
  name: string;
}

const person = new Person();
person.name = 'Jane';
```

### Members: Visibility

Class members also be given special modifiers which affect visibility.

There are three main visibility modifiers in TypeScript.

- public - (default) allows access to the class member from anywhere
- private - only allows access to the class member from within the class
- protected - allows access to the class member from itself and any classes that inherit it, which is covered in the inheritance section below

```ts
class Person {
  private name: string;

  public constructor(name: string) {
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}

const person = new Person('Jane');
console.log(person.getName()); // person.name isn't accessible from outside the class since it's private
```

> The `this` keyword in a class usually refers to the instance of the class. Read more about `this` [here](https://www.w3schools.com/js/js_this.asp).

### Parameter Properties

TypeScript provides a convenient way to define class members in the constructor, by adding a visibility modifiers to the parameter.

```ts
class Person {
  // name is a private member variable
  public constructor(private name: string) {}

  public getName(): string {
    return this.name;
  }
}

const person = new Person('Jane');
console.log(person.getName());
```

### Readonly

Similar to arrays, the `readonly` keyword can prevent class members from being changed.

```ts
class Person {
  private readonly name: string;

  public constructor(name: string) {
    // name cannot be changed after this initial definition, which has to be either at it's declaration or in the constructor.
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}

const person = new Person('Jane');
console.log(person.getName());
```

### Inheritance: Implements

Interfaces can be used to define the type a class must follow through the `implements` keyword.

```ts
interface Shape {
  getArea: () => number;
}

class Rectangle implements Shape {
  public constructor(
    protected readonly width: number,
    protected readonly height: number
  ) {}

  public getArea(): number {
    return this.width * this.height;
  }
}
```

> A class can implement multiple interfaces by listing each one after `implements`, separated by a comma like so: `class Rectangle implements Shape, Colored {`

### Inheritance: Extends

Classes can extend each other through the `extends` keyword. A class can only extends one other class.

```ts
interface Shape {
  getArea: () => number;
}

class Rectangle implements Shape {
  public constructor(
    protected readonly width: number,
    protected readonly height: number
  ) {}

  public getArea(): number {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  public constructor(width: number) {
    super(width, width);
  }

  // getArea gets inherited from Rectangle
}
```

### Override

When a class extends another class, it can replace the members of the parent class with the same name.

Newer versions of TypeScript allow explicitly marking this with the `override` keyword.

```ts
interface Shape {
  getArea: () => number;
}

class Rectangle implements Shape {
  // using protected for these members allows access from classes that extend from this class, such as Square
  public constructor(
    protected readonly width: number,
    protected readonly height: number
  ) {}

  public getArea(): number {
    return this.width * this.height;
  }

  public toString(): string {
    return `Rectangle[width=${this.width}, height=${this.height}]`;
  }
}

class Square extends Rectangle {
  public constructor(width: number) {
    super(width, width);
  }

  // this toString replaces the toString from Rectangle
  public override toString(): string {
    return `Square[width=${this.width}]`;
  }
}
```

> By default the `override` keyword is optional when overriding a method, and only helps to prevent accidentally overriding a method that does not exist. Use the setting `noImplicitOverride` to force it to be used when overriding.

### Abstract Classes

Classes can be written in a way that allows them to be used as a base class for other classes without having to implement all the members. This is done by using the `abstract` keyword. Members that are left unimplemented also use the `abstract` keyword.

```ts
abstract class Polygon {
  public abstract getArea(): number;

  public toString(): string {
    return `Polygon[area=${this.getArea()}]`;
  }
}

class Rectangle extends Polygon {
  public constructor(
    protected readonly width: number,
    protected readonly height: number
  ) {
    super();
  }

  public getArea(): number {
    return this.width * this.height;
  }
}
```

> Abstract classes cannot be directly instantiated, as they do not have all their members implemented.

[🔼 Back to top](#typescript-tutorial)

## TypeScript Basic Generics

Generics allow creating 'type variables' which can be used to create classes, functions & type aliases that don't need to explicitly define the types that they use.

Generics makes it easier to write reusable code.

### Functions

Generics with functions help make more generalized methods which more accurately represent the types used and returned.

```ts
function createPair<S, T>(v1: S, v2: T): [S, T] {
  return [v1, v2];
}
console.log(createPair<string, number>('hello', 42)); // ['hello', 42]
```

> TypeScript can also infer the type of the generic parameter from the function parameters.

### Classes

Generics can be used to create generalized classes, like [Map](https://www.w3schools.com/js/js_maps.asp).

```ts
class NamedValue<T> {
  private _value: T | undefined;

  constructor(private name: string) {}

  public setValue(value: T) {
    this._value = value;
  }

  public getValue(): T | undefined {
    return this._value;
  }

  public toString(): string {
    return `${this.name}: ${this._value}`;
  }
}

let value = new NamedValue<number>('myNumber');
value.setValue(10);
console.log(value.toString()); // myNumber: 10
```

> TypeScript can also infer the type of the generic parameter if it's used in a constructor parameter.

### Type Aliases

Generics in type aliases allow creating types that are more reusable.

```ts
type Wrapped<T> = { value: T };

const wrappedValue: Wrapped<number> = { value: 10 };
```

> This also works with interfaces with the following syntax: `interface Wrapped<T> {`

### Default Value

Generics can be assigned default values which apply if no other value is specified or inferred.

```ts
class NamedValue<T = string> {
  private _value: T | undefined;

  constructor(private name: string) {}

  public setValue(value: T) {
    this._value = value;
  }

  public getValue(): T | undefined {
    return this._value;
  }

  public toString(): string {
    return `${this.name}: ${this._value}`;
  }
}

let value = new NamedValue('myNumber');
value.setValue('myValue');
console.log(value.toString()); // myNumber: myValue
```

### Extends

Constraints can be added to generics to limit what's allowed. The constraints make it possible to rely on a more specific type when using the generic type.

```ts
function createLoggedPair<S extends string | number, T extends string | number>(
  v1: S,
  v2: T
): [S, T] {
  console.log(`creating pair: v1='${v1}', v2='${v2}'`);
  return [v1, v2];
}
```

> This can be combined with a default value.

[🔼 Back to top](#typescript-tutorial)

## TypeScript Utility Types

TypeScript comes with a large number of types that can help with some common type manipulation, usually referred to as utility types.

This chapter covers the most popular utility types.

### Partial

`Partial` changes all the properties in an object to be optional.

```ts
interface Point {
  x: number;
  y: number;
}

let pointPart: Partial<Point> = {}; // `Partial` allows x and y to be optional
pointPart.x = 10;
```

### Required

`Required` changes all the properties in an object to be required.

```ts
interface Car {
  make: string;
  model: string;
  mileage?: number;
}

let myCar: Required<Car> = {
  make: 'Ford',
  model: 'Focus',
  mileage: 12000, // `Required` forces mileage to be defined
};
```

### Record

`Record` is a shortcut to defining an object type with a specific key type and value type.

```ts
const nameAgeMap: Record<string, number> = {
  Alice: 21,
  Bob: 25,
};
```

> `Record<string, number>` is equivalent to `{ [key: string]: number }`

### Omit

`Omit` removes keys from an object type.

```ts
interface Person {
  name: string;
  age: number;
  location?: string;
}

const bob: Omit<Person, 'age' | 'location'> = {
  name: 'Bob',
  // `Omit` has removed age and location from the type and they can't be defined here
};
```

### Pick

`Pick` removes all but the specified keys from an object type.

```ts
interface Person {
  name: string;
  age: number;
  location?: string;
}

const bob: Pick<Person, 'name'> = {
  name: 'Bob',
  // `Pick` has only kept name, so age and location were removed from the type and they can't be defined here
};
```

### Exclude

`Exclude` removes types from a union.

```ts
type Primitive = string | number | boolean;
const value: Exclude<Primitive, string> = true; // a string cannot be used here since Exclude removed it from the type.
```

### ReturnType

`ReturnType` extracts the return type of a function type.

```ts
type PointGenerator = () => { x: number; y: number };
const point: ReturnType<PointGenerator> = {
  x: 10,
  y: 20,
};
```

### Parameters

`Parameters` extracts the parameter types of a function type as an array.

```ts
type PointPrinter = (p: { x: number; y: number }) => void;
const point: Parameters<PointPrinter>[0] = {
  x: 10,
  y: 20,
};
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Keyof

`keyof` is a keyword in TypeScript which is used to extract the key type from an object type.

### `keyof` with explicit keys

When used on an object type with explicit keys, `keyof` creates a union type with those keys.

```ts
interface Person {
  name: string;
  age: number;
}
// `keyof Person` here creates a union type of "name" and "age", other strings will not be allowed
function printPersonProperty(person: Person, property: keyof Person) {
  console.log(`Printing person property ${property}: "${person[property]}"`);
}
let person = {
  name: 'Max',
  age: 27,
};
printPersonProperty(person, 'name'); // Printing person property name: "Max"
```

### `keyof` with index signatures

`keyof` can also be used with index signatures to extract the index type.

```ts
type StringMap = { [key: string]: unknown };
// `keyof StringMap` resolves to `string` here
function createStringPair(property: keyof StringMap, value: string): StringMap {
  return { [property]: value };
}
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Null & Undefined

TypeScript has a powerful system to deal with `null` or `undefined` values.

> By default `null` and `undefined` handling is disabled, and can be enabled by setting `strictNullChecks` to true. The rest of this page applies for when `strictNullChecks` is enabled.

### Types

`null` and `undefined` are primitive types and can be used like other types, such as `string`.

```ts
let value: string | undefined | null = null;
value = 'hello';
value = undefined;
```

> When `strictNullChecks` is enabled, TypeScript requires values to be set unless `undefined` is explicitly added to the type.

### Optional Chaining

Optional Chaining is a JavaScript feature that works well with TypeScript's null handling. It allows accessing properties on an object, that may or may not exist, with a compact syntax. It can be used with the `?.` operator when accessing properties.

```ts
interface House {
  sqft: number;
  yard?: {
    sqft: number;
  };
}
function printYardSize(house: House) {
  const yardSize = house.yard?.sqft;
  if (yardSize === undefined) {
    console.log('No yard');
  } else {
    console.log(`Yard is ${yardSize} sqft`);
  }
}

let home: House = {
  sqft: 500,
};

printYardSize(home); // Prints 'No yard'
```

### Nullish Coalescence

Nullish Coalescence is another JavaScript feature that also works well with TypeScript's null handling. It allows writing expressions that have a fallback specifically when dealing with `null` or `undefined`. This is useful when other falsy values can occur in the expression but are still valid. It can be used with the `??` operator in an expression, similar to using the `&&` operator.

```ts
function printMileage(mileage: number | null | undefined) {
  console.log(`Mileage: ${mileage ?? 'Not Available'}`);
}

printMileage(null); // Prints 'Mileage: Not Available'
printMileage(0); // Prints 'Mileage: 0'
```

### Null Assertion

TypeScript's inference system isn't perfect, there are times when it makes sense to ignore a value's possibility of being `null` or `undefined`. An easy way to do this is to use casting, but TypeScript also provides the `!` operator as a convenient shortcut.

```ts
function getValue(): string | undefined {
  return 'hello';
}
let value = getValue();
console.log('value length: ' + value!.length);
```

> Just like casting, this can be unsafe and should be used with care.

### Array bounds handling

Even with `strictNullChecks` enabled, by default TypeScript will assume array access will never return undefined (unless undefined is part of the array type).

The config `noUncheckedIndexedAccess` can be used to change this behavior.

```ts
let array: number[] = [1, 2, 3];
let value = array[0]; // with `noUncheckedIndexedAccess` this has the type `number | undefined`
```

[🔼 Back to top](#typescript-tutorial)

## TypeScript Definitely Typed

NPM packages in the broad JavaScript ecosystem doesn't always have types available.

Sometimes the projects are no longer maintained, and other times they aren't interested in, agree with, or have time to use TypeScript.

### Using non-typed NPM packages in TypeScript

Using untyped NPM packages with TypeScript will not be type safe due to lack of types.

To help TypeScript developers use such packages, there is a community maintained project called [Definitely Typed](http://definitelytyped.org).

Definitely Typed is a project that provides a central repository of TypeScript definitions for NPM packages which do not have types.

```shell
npm install --save-dev @types/jquery
```

No other steps are usually needed to use the types after installing the declaration package, TypeScript will automatically pick up the types when using the package itself.

> Editors such as Visual Studio Code will often suggest installing packages like these when types are missing.

[🔼 Back to top](#typescript-tutorial)

## Leetcode Problems & Solutions

Here are the list of problems and includes solutions with TypeScript code:

- [2235. Add Two Integers](https://github.com/Mengsreang-Chhoeung/typescript-tutorial/tree/main/src/leetcode/2235-add-two-integers)

[🔼 Back to top](#typescript-tutorial)

### 📜 References

- [W3Schools](https://www.w3schools.com/typescript)

- [TypeScript Documentation](https://www.typescriptlang.org/docs)

- [Leetcode](https://leetcode.com)

### 🤝 Contributors

- Mengsreang-Chhoeung [@mengsreang_dev](https://twitter.com/mengsreang_dev)
