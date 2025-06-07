# TypeScript Definitely Typed

NPM packages in the broad JavaScript ecosystem doesn't always have types available.

Sometimes the projects are no longer maintained, and other times they aren't interested in, agree with, or have time to use TypeScript.

## Using non-typed NPM packages in TypeScript

Using untyped NPM packages with TypeScript will not be type safe due to lack of types.

To help TypeScript developers use such packages, there is a community maintained project called [Definitely Typed](http://definitelytyped.org).

Definitely Typed is a project that provides a central repository of TypeScript definitions for NPM packages which do not have types.

```shell
npm install --save-dev @types/jquery
```

No other steps are usually needed to use the types after installing the declaration package, TypeScript will automatically pick up the types when using the package itself.

> Editors such as Visual Studio Code will often suggest installing packages like these when types are missing.

# 📜 References

- [TypeScript Definitely Typed](https://www.w3schools.com/typescript/typescript_definitely_typed.php)

---

<a href="./typescript-null.md">◀ Previous</a>&nbsp;&nbsp;<a href="./typescript-5-updates.md">Next ▶</a>
