# CJL Language
![image](https://user-images.githubusercontent.com/91914454/137986186-43a28636-42b9-4750-aa90-6805c9058f01.png)

## CJL language features
* Strong type convertions
* Strong out of range control TODO: ?
* Unique references and copies of references
* All is a class, classes as single files
* All classes are public, modifiers are used for fields and methods
* All primitives are initialized with zeros if another value wasn't provided
* Arrays have fixed size determined during the definition
* **Safety is a priority!**

## Primitives
```
All are 64 bits long:
int
char
double
```
**Optional**
```
bool
```

## Complex types
```
T[5] a;
class T;
String str;
```

Example of using array
```
int[] arrA = {1, 2, 3};		// correct
int[100] arrB;			// correct, initialized with 0
```

<!-- ## Some constants
```
errptr = #0x0;
something = 1;
nothing = 0;
``` -->

## Some rules
* All primitives are initialized with 0 values if not provided with another value. TODO: Classes
```
int a;		// correct, a == 0 
int b = 1;	// b == 1
```
* Fields of the class are accessed with `this.method` syntax. Methods are called without using `this`.
Here `this` is a reference to the object itself.
```
class Cl {
public:
	const int num;
	Cl() {
		this.num = 21;
	}
	dummy() const -> int {
		return num;		// error: use this
		return this.num;	// correct
	}
	printNumber() const -> void {
		print(dummy());
	}
}
```
* Keywords are added to the function signature in the following order:
```
static, const, override
```
* For variables declaration the following order of keywords is used:
```
static, const
```
* `and` and `or` are used instead of `&&` and `||` respectively

<!-- ## type convertions
```

``` -->

## References
All objects are created with a call to constructor. References (as well as primitives) are copied when passing to
other methods. There are two types of references: strong and weak (the latter are marked for GC to be cleaned).
```
Object obj = Object(arg1, arg2, ....);
```
Example of passing the object (by reference) into method:
```
public:
	changeNum(Object obj) static const -> int {
		obj.num = 20;	// obj.num = 20 in the main()
		obj = new Object(100);	// obj from main() is intact
		return obj.num;		// 100 
	}

	main(String[] args]) static -> int {
		Object obj = new Object(10);	// obj.num = 10
		print(obj.num);		// prints 20
	}
```

## Loops
* For:
```
for (<single variable definition>; <predicat>; <operation for next>) {
	....
}
```
* While:
```
while(<predicat>) {
	....
}
```


## Class inheritance
Only public inheritance is available. `override` keyword is written in the end of the method signature
for all methods which produce override.
fileA.cjl:
```
class Cl1 {
public:
    int a = 0;	// error: all variables but static are initialized in constructors
	int a;		// correct
    static String classname = "Cl1";
    do_something() -> double {
		....
	}
    work() const -> void {
		....
	}
protected:
	....
private:
	....
};
```
fileB.cjl:
```
class Cl2 inherits Cl1 {
public:
	work() const override -> void {
		....
	}
}
```
