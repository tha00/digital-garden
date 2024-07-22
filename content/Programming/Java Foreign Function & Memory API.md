---
title: "Java Foreign Function & Memory API"
draft: false
tags:
  - 
---
Terminology:
* *downcall method handle*: call native functions from Java
* *upcall stub*: call Java functions from native code

Ingedients:
* `Linker.nativeLinker()` returns a platform-specific [Linker](https://docs.oracle.com/en%2Fjava%2Fjavase%2F22%2Fdocs%2Fapi%2F%2F/java.base/java/lang/foreign/Linker.html)
	* produces method handles given the adress of functions and their descriptors
* `SymbolLookup` retrieves the adress of a symbol in a library
	* symbols can be functions or global variables
	* the adress of a symbol is modelled as a zero-length `MemorySegment`
	* `Linker#defaultLookup` returns the standard C library symbols loaded with the Java runtime
	* `SymbolLookup#libraryLookup` can load other libraries

Example:
```java
public static void main(String[] args) throws Throwable {  
    // default lookup contains standard C library loaded with the Java runtime
    Linker linker = Linker.nativeLinker();  
    SymbolLookup stdlib = linker.defaultLookup();  
  
    // search for `strlen` and describe its input and output types  
    MemorySegment strlenAddress = stdlib.find("strlen").orElseThrow();  
    FunctionDescriptor descriptor = FunctionDescriptor.of(  
        ValueLayout.JAVA_LONG,    // result
        ValueLayout.ADDRESS       // input
    );  
  
    // method handle represents native function in Java  
    MethodHandle strlen = linker.downcallHandle(strlenAddress, descriptor);  
  
    // allocate off-heap memory and call function  
    try (Arena arena = Arena.ofConfined()) {  
        MemorySegment str = arena.allocateFrom("Hello");  
        long len = (long) strlen.invoke(str);  
        System.out.println(STR."Length = \{len}");  // 5
    }  
}
```


References:
* [JEP 454: Foreign Function & Memory API](https://openjdk.org/jeps/454)  
* [Java 22 release notes](https://docs.oracle.com/en/java/javase/22/core/foreign-function-and-memory-api.html)
* Javadoc [Linker](https://docs.oracle.com/en%2Fjava%2Fjavase%2F22%2Fdocs%2Fapi%2F%2F/java.base/java/lang/foreign/Linker.html):  contains `strlen` example  
* Javadoc [SymbolLookup](https://docs.oracle.com/en/java/javase/22/docs/api/java.base/java/lang/foreign/SymbolLookup.html):  explains how native methods are represented in Java
* [Blog post](https://internalpointers.com/post/journey-across-static-dynamic-libraries) by "Internal Pointers" about static and dynamic libraries
* [Blog post](http://clarkkromenaker.com/post/library-dynamic-loading-mac/) by Clark Kromenaker about dynamic library loading on MacOS
