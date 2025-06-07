# TypeScript Keyof

`keyof` is a keyword in TypeScript which is used to extract the key type from an object type.

## `keyof` with explicit keys

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

## `keyof` with index signatures

`keyof` can also be used with index signatures to extract the index type.

```ts
type StringMap = { [key: string]: unknown };
// `keyof StringMap` resolves to `string` here
function createStringPair(property: keyof StringMap, value: string): StringMap {
  return { [property]: value };
}
```

# 📜 References

- [TypeScript Keyof](https://www.w3schools.com/typescript/typescript_keyof.php)

---

<a href="./typescript-utility-types.md">◀ Previous</a>&nbsp;&nbsp;<a href="./typescript-null.md">Next ▶</a>
