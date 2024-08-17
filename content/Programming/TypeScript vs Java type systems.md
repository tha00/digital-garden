---
title: TypeScript vs Java type systems
draft: false
tags:
---

Java's type system is *nominal*, i.e.
```java
class A {
  String x;
}

class B {
  String x;
}
```
are different types, we can't assign a `B` to an `A` variable.

TypeScript's type system is *structural*, i.e. 
```ts
class A {
  x: string;
}

class B {
  x: string;
}
```
are equal types, that is `let a: A = new B();` is allowed.

Anything that has a `string` property named `x` qualifies as an `A`.

### Comparison

Nominal types are safer as they prevent accidental type equivalence. Structural types are more flexible, e.g. new new super-types can be created without adapting the existing subtypes.

### Mimicking nominal types in TypeScript

Add a literal field to distinguish strucurally equal types:
```ts
type ValidatedString = string & { __brand: "validated" };

const print = (s: ValidatedString) => {
  console.log(s);
};

print('Plain string')  // compile error
print('Plain string' as ValidatedString)
```
We tell TypeScript, which nominal variant the object is by casting, i.e. we need to be careful at the "entrypoints"  into nominal types.

References:
* [GitHub issue](https://github.com/Microsoft/TypeScript/issues/202) discussing nominal types for TypeScript (~500 comments)
* Mimicking nominal types in TypeScript using [brands](https://www.typescriptlang.org/play#example/nominal-typing)
* [Blog post](https://michalzalecki.com/nominal-typing-in-typescript/) by Michal Zalecki comparing different approaches to nominal types in TypeScript