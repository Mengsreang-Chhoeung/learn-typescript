# TypeScript Null & Undefined

TypeScript has a powerful system to deal with `null` or `undefined` values.

> By default `null` and `undefined` handling is disabled, and can be enabled by setting `strictNullChecks` to true. The rest of this page applies for when `strictNullChecks` is enabled.

## Types

`null` and `undefined` are primitive types and can be used like other types, such as `string`.

```ts
let value: string | undefined | null = null;
value = 'hello';
value = undefined;
```

> When `strictNullChecks` is enabled, TypeScript requires values to be set unless `undefined` is explicitly added to the type.

## Optional Chaining

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

## Nullish Coalescence

Nullish Coalescence is another JavaScript feature that also works well with TypeScript's null handling. It allows writing expressions that have a fallback specifically when dealing with `null` or `undefined`. This is useful when other falsy values can occur in the expression but are still valid. It can be used with the `??` operator in an expression, similar to using the `&&` operator.

```ts
function printMileage(mileage: number | null | undefined) {
  console.log(`Mileage: ${mileage ?? 'Not Available'}`);
}

printMileage(null); // Prints 'Mileage: Not Available'
printMileage(0); // Prints 'Mileage: 0'
```

## Null Assertion

TypeScript's inference system isn't perfect, there are times when it makes sense to ignore a value's possibility of being `null` or `undefined`. An easy way to do this is to use casting, but TypeScript also provides the `!` operator as a convenient shortcut.

```ts
function getValue(): string | undefined {
  return 'hello';
}
let value = getValue();
console.log('value length: ' + value!.length);
```

> Just like casting, this can be unsafe and should be used with care.

## Array bounds handling

Even with `strictNullChecks` enabled, by default TypeScript will assume array access will never return undefined (unless undefined is part of the array type).

The config `noUncheckedIndexedAccess` can be used to change this behavior.

```ts
let array: number[] = [1, 2, 3];
let value = array[0]; // with `noUncheckedIndexedAccess` this has the type `number | undefined`
```

# 📜 References

- [TypeScript Null & Undefined](https://www.w3schools.com/typescript/typescript_null.php)

---

<a href="./typescript-keyof.md">◀ Previous</a>&nbsp;&nbsp;<a href="./typescript-definitely-typed.md">Next ▶</a>
