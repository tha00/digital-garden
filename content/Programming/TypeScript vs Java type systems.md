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
