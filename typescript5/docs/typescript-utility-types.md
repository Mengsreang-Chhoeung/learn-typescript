# TypeScript Utility Types

TypeScript comes with a large number of types that can help with some common type manipulation, usually referred to as utility types.

This chapter covers the most popular utility types.

## Partial

`Partial` changes all the properties in an object to be optional.

```ts
interface Point {
  x: number;
  y: number;
}

let pointPart: Partial<Point> = {}; // `Partial` allows x and y to be optional
pointPart.x = 10;
```

## Required

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

## Record

`Record` is a shortcut to defining an object type with a specific key type and value type.

```ts
const nameAgeMap: Record<string, number> = {
  Alice: 21,
  Bob: 25,
};
```

> `Record<string, number>` is equivalent to `{ [key: string]: number }`

## Omit

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

## Pick

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

## Exclude

`Exclude` removes types from a union.

```ts
type Primitive = string | number | boolean;
const value: Exclude<Primitive, string> = true; // a string cannot be used here since Exclude removed it from the type.
```

## ReturnType

`ReturnType` extracts the return type of a function type.

```ts
type PointGenerator = () => { x: number; y: number };
const point: ReturnType<PointGenerator> = {
  x: 10,
  y: 20,
};
```

## Parameters

`Parameters` extracts the parameter types of a function type as an array.

```ts
type PointPrinter = (p: { x: number; y: number }) => void;
const point: Parameters<PointPrinter>[0] = {
  x: 10,
  y: 20,
};
```

# 📜 References

- [TypeScript Utility Types](https://www.w3schools.com/typescript/typescript_utility_types.php)

---

<a href="./typescript-basic-generics.md">◀ Previous</a>&nbsp;&nbsp;<a href="./typescript-keyof.md">Next ▶</a>
