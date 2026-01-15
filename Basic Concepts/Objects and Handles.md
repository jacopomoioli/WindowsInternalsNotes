# Object and Handles
## Kernel Object
Single, run time instance of a statically defined object type.

Object type is composed by
- a system defined data type
- object methods: functions that operate on instances of the data type
	- read or change object attributes
- objects attributes
	- field that partially defines the object state

Internal structure of an object is opaque: you cant directly read or change data inside an object, but call the object service => ENCAPSULATION

Handle: single instance of an object. instead of using the pointer to the instance, it's a number that acts as an interface.