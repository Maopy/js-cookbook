# Types in JS

## Type system

In programming languages, a **type system** is a set of rules that assigns a property called type to the various constructs of a computer program, such as variables, expressions, functions or modules. These types formalize and enforce the otherwise implicit categories the programmer uses for algebraic data types, data structures, or other components \(e.g. "string", "array of float", "function returning boolean"\). The main purpose of a type system is to reduce possibilities for bugs in computer programs by defining interfaces between parts of a computer program, and then checking that the parts have been connected in a consistent way. This checking can happen statically \(at compile time\), dynamically \(at run time\), or as a combination of static and dynamic checking. Type systems have other purposes as well, such as expressing business rules, enabling certain compiler optimizations, allowing for multiple dispatch, providing a form of documentation, etc.

A type system associates a type with each computed value and, by examining the flow of these values, attempts to ensure or prove that no type errors can occur. The given type system in question determines exactly what constitutes a type error, but in general the aim is to prevent operations expecting a certain kind of value from being used with values for which that operation does not make sense \(logic errors\).Type systems are often specified as part of programming languages, and built into the interpreters and compilers for them.

### Fundamentals

A programming language must have occurrence to type check using the _type system_ whether at compile time or runtime, manually annotated or automatically inferred. Assigning a data type, termed _typing_, gives meaning to a sequence of bits such as a value in memory or some object such as a variable. The hardware of a general purpose computer is unable to discriminate between for example a memory address and an instruction code, or between a character, an integer, or a floating-point number, because it makes no intrinsic distinction between any of the possible values that a sequence of bits might mean. Associating a sequence of bits with a type conveys that meaning to the programmable hardware to form a _symbolic system_ composed of that hardware and some program.

An implementation of a _type system_ could in theory associate identifications called _data type_ \(a type of a value\), _class_ \(a type of an object\), and _kind_ \(_a type of a type_, or metatype\). A programming language compiler can also implement a _dependent type_ or an _effect system_, which enables even more program specifications to be verified by a type checker. 

