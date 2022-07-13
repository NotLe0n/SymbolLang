# SymbolCompiler
A programming language without words.

# Specification

## Table of Contents
- [SymbolCompiler](#symbolcompiler)
- [Specification](#specification)
	- [Table of Contents](#table-of-contents)
- [Variables](#variables)
	- [Declaration](#declaration)
	- [Types](#types)
	- [Examples:](#examples)
- [Operators](#operators)
- [Control Structures](#control-structures)
	- [Conditionals:](#conditionals)
		- [Single Branch:](#single-branch)
		- [Two Branches:](#two-branches)
		- [Multiple Branches:](#multiple-branches)
	- [Loops:](#loops)
		- [Constant:](#constant)
		- [Conditional:](#conditional)
		- [Iterative:](#iterative)
- [Functions:](#functions)
	- [Declaration:](#declaration-1)
	- [Calling:](#calling)
	- [Example:](#example)
- [Structs:](#structs)
	- [Declaration](#declaration-2)
- [Console IO:](#console-io)
	- [Printing:](#printing)
	- [Reading:](#reading)
- [Example Code:](#example-code)
	- [Fizzbuzz:](#fizzbuzz)
	- [Fibonacci:](#fibonacci)
	- [Multtable:](#multtable)


# Variables
## Declaration

```html
<type>_<number> = <statement>
```

## Types

* Integer Types (u = unsigned): `i<size>`, `u<size>`
* Floating Point Types: `f32`, `f64`
* String: `s`
* Char: `c`
* Array: `<non-array-type>[]`
* Void (Only allowed in return statements): `()`

## Examples:
```
i64_0 = -50000;
u8_0 = 32;
f32_0 = 2.5;
u1_0 = 0;
u1_1 = 1;
s_0 = "Hello World";
c[]_0 = ['h', 'i'];
u32[]_0 = 0...100;
=> ();
```

# Operators

|  Name  | Operator | Example |   |   Name  | Operator | Example  |   |   Name  | Operator | Example  |
|--------|----------|---------|---|---------|----------|----------|---|---------|----------|----------|
| plus   | 	 `+`	| `2 + 2` |   | eq      |  `==`    | `1 == 1` |   |Casting  |   `->`   | `u8_0 -> u32` |
| minus  | 	 `-`	| `6 - 4` |   | neq     |  `!=`    | `2 != 4` |   |Return   |   `=>`   |   `=> 5` |
| mult   | 	 `*`	| `10 * 5`|   | less    |  `<`     | `4 < 8`  |   |Break    |   `>\|`  ||
| div:   | 	 `/`	| `4 / 2` |   | greater |  `> `    | `100 > 2`|   |Continue |   `->>`  ||
| exp:   | 	 `^`	| `2 ^ 8` |   | AND     |  `&`     | `12 & 4` |   |Panic    |   `!`    | `!"AAAH"`|
| LShft  | 	 `<<`   | `4 << 2`|   | OR      |  `\|`    | `7 \| 3` |   |Memberaccess | `.`  |`S_0.u32_0`|
| RShft  | 	 `>>`   | `8 >> 3`|   | NOT     |  `~`     | `~5`     |   |Length   |   `#`    |`#u32[]_0`|
| inc    | 	 `++`   | `u8_0++`|   | XOR     |  `<>`    | `6 >< 3` |   |
| dec    | 	 `--`   | `u8_0--`|   | indexing|  `@`     | `u32[]_0 @ 1`|
| modulo | 	 `%`    | `4 % 2` |   | range   |   `...`  | `0...100`|   |

# Control Structures

## Conditionals:
### Single Branch:
```html
(<boolean expression>) ?:
	<statement>
	...
```
		
### Two Branches:
```html
(<boolean expression>) ?:
	<statement>
	...
~?:
	<statement>
	...
```
		
### Multiple Branches:
```html
(<boolean expression>) ?:
	<statement>
	...
~? & (<boolean expression>) ?:
	<statement>
	...
~?:
	<statement>
	...
```
	
## Loops:
### Constant:
```html
O(<loop count>):
	<statement>
	...
```
		
### Conditional:
```html
O(<boolean expression>) ?:
	<statement>
	...
```

### Iterative:
```html
O(<var decl> ->> <array or range>):
	<statement>
	...
```

# Functions:
## Declaration:
```html
F_<Func number>(<args as vars (optional)>) => <return type (optional)>:
	<statement>
	...
```

## Calling:
```html
F_<Func number>(<args>);
```

## Example:
```
F_0(u8_0, u8_1) => u8:
	=> u8_0 + u8_1;

> F_0(5, 2);
```

# Structs:
## Declaration
```
S_0:
	u32_0,
	u32_1,
	s_0,
``` 

# Console IO:
## Printing: 
```html
C< <expression>
```
## Reading: 
```html
C> <variable>
```

# Example Code:

## Fizzbuzz:
```
O(u8_0 ->> 0...100):
	u1_0 = (u8_0 % 3 == 0);
	u1_1 = (u8_0 % 5 == 0);

	(u1_0 & u1_1) ?:
		C< "Fizzbuzz";
	~? & (u1_0) ?:
		C< "Fizz";
	~? & (u1_1) ?:
		C< "Buzz";
	~?:
		C< u8_0;
```

## Fibonacci:
```
F_0(u32_0) => u32:
	(u32_0 <= 1) ?: 
		=> u32_0;
	=> (F_0(u32_0 - 2) + F_0(u32_0 - 1));
```

## Multtable:
```
O(u32_0 ->> 0...10) {
	O(u32_1 ->> 0...10) {
		C< u32_0 + " * " + u32_1 + " = " + u32_0 * u32_1;
		(u32_0 * u32_1 != 10 * 10)? {
			C< '\n';
		} 
	}
}
```