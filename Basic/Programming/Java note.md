# Conception
## Java technology
Java platform: my program -> hardware-based program / 机器码 (machine code, native code)
 - Java Virtual Machine
 - Java Application Programming interface (API)
## Language
object-oriented programming: 
 - real world object: two characteristics, state and behavior
 - software object:
	 - state: fields/variables
	 - behavior: methods/functions

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

package: a namespace that organizes classes and interfaces by functionality

Application Programming interface (API)

example template:
1. class: fields and methods
2. interface: define its behavior
	 - require the class to implement it
	 - omit some methods and see the error

static method: the methods can not be changed by objects' features