# TypeScript Union Types

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

# 📜 References

- [TypeScript Union Types](https://www.w3schools.com/typescript/typescript_union_types.php)

---

<a href="./typescript-aliases-interfaces.md">◀ Previous</a>&nbsp;&nbsp;<a href="./typescript-functions.md">Next ▶</a>
