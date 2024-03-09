# To do list

- [x] Getting Started
- [x] Learning the Java Language
	- [x] Object-Oriented Programming Concepts
	- [ ] Language Basics
	- [ ] Classes and Objects
	- [ ] Annotations
	- [ ] Interfaces and Inheritance
	- [ ] Numbers and Strings
	- [ ] Generics
	- [ ] Packages
- [ ] Essential Classes
	- [ ] Exceptions
	- [ ] Basic I/O
	- [ ] Concurrency
	- [ ] The Platform Environment
	- [ ] Regular Expressions
- [ ] Collections
	- [ ] Introduction
	- [ ] Interfaces
	- [ ] Aggregate Operations
	- [ ] Implementations
	- [ ] Algorithms
	- [ ] Custom Implementations
	- [ ] Interoperability
- [ ] The Reflection API
	- [ ] Classes
	- [ ] Members
	- [ ] Arrays and Enumerated Types

# Java technology

Java platform: my program -> hardware-based program / 机器码 (machine code, native code)
 - Java Virtual Machine
 - Java Application Programming interface (API)

IDE:
- multiple cursor: [Alt] + [Shift]

# Language

## Object-Oriented

object-oriented programming: two characteristics
 - real world object: state and behavior
 - software object: including members below
	 - state: variables/fields
	 - behavior: methods/functions
		 - static: cannot access object's variables
			 - mix of static and non-static methods
		 - non-static: instance
			 - invocation: `new` to create a specific instance, cannot using class name

fundamental principle: data encapsulation
 - hiding internal state, accessing it only through publicly exposed metods
 - requiring all interaction
 - all of above state performed through an object’s methods

class: blueprint from which individual objects are created, blueprint for a software object

inheritance: classes to inherit commonly used state and behabior from other classes
 - superclass: hierarchy, define the common behavior
	 - each class is allowed to have one direct superclass
	 - each superclass has the potential for an unlimited number of subclasses
 - subclass: use the extends keywords to inherit the common behaviors

interface: a collection of methods with no implementation
 - method is the objects’ interface with the outside world
 - a class was declared by `implement` the interface

package: a namespace that organizes classes and interfaces by functionality
- like a folder:
	- html pages
	- images
	- scripts or applications
- Application Programming interface (API): an enormous class library, use a set of packages for our own application
	- packages: general-purpose programming:
		- `String`: state and behavior for character strigns
		- `File`: create, delete, inspect, compare, or modify a file on the filesystem
		- `Socket`: creation and use of network sockets
		- GUI objects: graphical user interfaces
			- control buttons
			- check boxes

example template:
1. class: fields and methods
2. interface: define its behavior
	 - require the class to implement it
	 - omit some methods and see the error

class -> variable: Declaration
class -> Object: Instantiation
 - `new`
Object -> variable: Assignment
member of Object: Invocation
 - `Variable_of_Object.Member`

homework:
- questions:
	1. states and behaviors
	2. state stored in fields
	3. behavior exposed through methods
	4. encapsulation
	5. class is a blueprint for object
	6. superclass, subclass, `extends`
	7. interface: a collection of methods with no implementation
	8. package: organizes classes and interfaces by functionality
	9. application package interface
- exersice
	1. cup

## Language Basics

variables:
- Instance Variable (non-staric fields): store individual states
	- *fields* declared without the `static` keyword
	- also known as *instance variables*: their values are unique to each *instance* of a class/object
- Class Variables (static fields): 
	- *field* declared with the `static` modifier, which tells the compiler: 
		- there is exactly one copy of this variable in existence, regardless of how many times the class has been instantiated
	- `final` keyword: indicates that the variable will never change
- Local Variables: where a method stores its temporary state
	- syntax: similar to declaring a *field*
	- no special keyword designating a *variable as local*
		- location: between the openting and closing braces of a method
		- not accessible from the classes, aside from that in which they are declared
	- an uninitialized local variable will never be assigned a default value
- Parameters: always classified as *variables* not *fields*
	- `args` variable is the parameter to the `main` method
	- applies to other parameter-accepting constructs: constructors, exception handlers
- general guidlines:
	- fields in general: fields, excluding local variables and parameters
	- all of the above: variables
	- member: collective calling of a type's field, methods, and nested types

variable naming: unicode letters and digits
- beginning: letter, " $ " (avoid) , " _ " (discouraged)
- subsequent characters: letter, digits, " $ ", " _ "
	- not be a key word or reserved word
- convention: lowercase letters of the first word, capitalize the first letter of each subsequent word
	- variable stores a constant value: `static final`, capitalize every letter, separating subsequent words with " _ "

primitive data types:
- declare: statically-typed programming language
	- state: type, name
- 8 *primitive data types*:
	- `byte`: 8-bit
		- minimum value of -128; maximum value of 127 (inclusive)
		- memory saving: memory in large arrays
		- in place of `int` where their limits helps ot clarify your code
		- serve as a form of documentation
		- default value: 0
	- `short`: 16-bit
		- minimum value of -32,768; maximum value of 32,767 (inclusive)
		- memory saving: memory in large arrays
		- default value: 0
	- `int`: 32-bit
		- minimue value of $-2^{31}$; maximum value of $2^{31}-1$
		- Java SE 8: unsigned 32-bit integer
			- minimum value of 0; maximum value of $2^{32}-1$
			- `integer` class: use `int` data type as an unsigned integer
			- arithmetic operations: `compareUnsigned`, `divideUnsigned`
		- default value: 0
	- `long`: 64-bit
		- minimum value of $-2^{63}$; maximum value of $2^{63}-1$
		- Java SE 8: unsigned 64-bit long
			- minimum value of 0; maximum value of $2^{64}-1$
			- arithmetic operations: `compareUnsigned`, `divideUnsigned`
		- default value: 0L
	- `float`: single-precision 32-bit IEEE 754 floating point
		- specification: Floating-Point Types, Formats, Values section
		- save memory: `byte` and `short`
		- never be used for precise value: like currency, use the `java.math .BigDecimal` class, Numbers and Strings section
		- default value: 0.0f
	- `double`: double-precision 64-bit IEEE 754 floating point
		- specification: Floating-Point Types, Formats, Values section
		- default choice of decimal values
		- never be used for precise value: like currency
		- default value: 0.0d
	- `boolean`: `true` or `false`
		- size: not precissely defined, providing 1-bit information
		- default value:  `false`
	- `char`: single 16-bit Unicode character
		- minimum value of `'\u0000'` (or 0); maximum value of `'\uffff'` (or 65,535 inclusive)
		- default value: `'\u0000'`
- special support data type: character `strings`
	- via `java.lang.String` class
	- *immutable*: once created, their values cannot be changed
	- Simple Data Objects section
	- default value: null

*literal*: the source code representation of a fixed value
- properties:
	- without requiring computation
	- assign a literal to a variable of a prmitive type without `new`
		- not objects created from class
- integer literals:
	- `long` literals: create value of type `long` that exceed the range of `int`
		- ends with the letter `L`
	- `int` literals: create value of the integral types `byte, short, int, long`
	- expressed by number systems: `26`
		- Decimal `26`
		- Hexadecimal `0x1a`
		- Binary `0b11010`
- floating-point literals:
	- `float`: end with letter `F`
	- `double`: end with letter `D`
	- expressed using `E` for scientific notation
- character and string literals: 
	- Unicode (UTF-16) characters: `char` and `String`
		- Unicode escape: `\u0108`, `S\u00ED Se\u00F1or`
		- `char` literals: single quotes
		- `String` literals: double quotes
	- special escape sequences:
		- `\b`(backspace), `\t`(tab), `\n`(line feed), `\f`(form feed), `\r`(carriage return)
		- `\"`(double quote), `\'`(single quote), `\\`(backslash)
		- `null`
			- do with: testing for its presence
- *class literal*
	- taking a type name and appending `.class`
	- `String.class`: refers to the object (of type `Class`) that represents the type itself
- numeric literals: underscore characters
	- appear anywhere between digits (only)
	- separate groups of digits: improve the readability of our code

arrays: a container object that holds a fixed number of values of a single type
- length: established when the array is created
	- fixed after creation
- *element*: each item in an array
- numerical *index/indices*: access each element
	- numbering begins with 0 (the end index less than the elements' length for 1)
- use:
	1. declaring: a variable to refer to an array
		- type: `type[]`
	2. creating, initializing: 
		- with the `new` operator
		- directly: show all
	3. accessing
- *multidimensional array* (an array of arrays): using two or more sets of brackets
- array manipulations: copying, sorting, searching arrays in the `java.util.Arrays` class
	- `copyOfRange` method of the `java.util.Arrays` class
		- initial index inclusively, final index  exclusively
	- other methods: 
		- `binarySearch`
		- `equals`
		- `fill`
		- `sort`, `parallelSort`
		- `stream`
		- `toString`

list<>: can be modified after declaration
```
List<String> list = new ArrayList<String>();  
list.add("awk -F'\\\\t' '$3 == \\\"repeat_region\\\" {split($9, a, \\\";\\\"); for (i in a) {split(a[i], b, \\\"=\\\"); if (b[1] == \\\"ID\\\") TE_id = b[2];}  print $1, $4-1, $5, TE_id, \\\".\\\", $7}' chr1A.gff3 > annotations.bed\", \n");  
list.add("gff2bed <JM44.repeat.masked.gff > annotation.bed");  
list.add("bedtools getfasta -s -fi JM44.repeat.masked.fasta -bed annotation.bed -fo teseq.fasta");  
list.add("seqkit stats teseq.fasta");  
list.add("python DataProcessing.py > call.txt");  
list.add("bedtools merge -i annotation.bed > merge.bed");  
String[] seqProcessing = list.toArray(new String[list.size()]);
```

operators: special symbols that perform operations on one, two, or three *operands*, and then return a result, precedence high to low
1. postfix: `expr++, expr--`
2. unary: `++expr --expr +expr -expr ~ !`
	- require only one operand
	- preform operations a value by one
	- negating an expression
	- inverting the value of a boolean
1. arithmetic:
	1. multiplicative: `* / %`
	2. additive: `+ -`
2. shift: `<< >> >>>`
3. relational: `< > <= >= instanceof`
	- type comparison operator: `instanceof`
		- compares an object to a specified type
1. equality: `== !=`
2. bitwise AND: `&`
3. bitwise exclusive OR: `^`
4. bitwise inclusive OR: `|`
5. conditional:
	1. logical/conditional AND: `&&`
	2. logical/conditional OR: `||`
	3. ternary (if-then-else): `? :`
		- use 3 operands
6. assignment: `= += -= *= /= %= &= ^= |= <<= >>= >>>=`
	- used on objects: assign object references
	- compound assignments

problem: 
- unary: +expr ~
- shift
- bitwise
- ternary

expressions, statements, and blocks

control flow statements