---
geometry: margin=2cm
author:
- AB Paxtor Garcia
date: '10/2/2023'
title: 'Compilers 1'
numbersections: true
---

# Compilers Part 1

## How do programming languages run

1. Interpreted Code

Input -> Interpreter -> Program output

2. Compiled

Input -> Compiler (Translate to Intermediate Language) -> Interpreter -> Program Output

Transpiled/Transpiled: High Level to High Level nuance, but mostly the same as compile

 ##  Compiler in focus

Input -> Tokenizer/Lexer (Tokens) -> Parser (groups tokens as a tree-like DS; Outputs a Abstract Syntax Tree) ->  TypeChecker (Sytnax Checker; Annnotates AST with Data Types) -> Code Generator -> Output


Input

Tokenizer
- Split into tokens (if, while, for)\

Parser
- Forms an Abstract Syntax Tree (AST) from the tokens

TypeChecker
- Vibe checks if the data types.
  - i.e.
    - int x = "foo"; // this is bad int != String

Code Generator
- Is the part which can be optimized 

Output


## Linguistics in Compilers

### Backus-Naur Form 

digit ::= '1' | '0'
number ::= digit | number 
expression ::= number | expression '+' expression

examples numbers:
0
1
01
191

example expreessions:
1101
101 + 110
(1 + 111) + (01 + 10)

### Parsing a Grammer/BNF

#### Language Design

- Integers and Bools
- Declare and init vars
- Arithmetic/Logical Operations

Grammar:
````
var is a Variable
type ::= `int` | `bool`
vardec ::= `(` `vardec` type var expression `)`
expression ::= num | `true` | `false` | var |  `(` op expression expression `)`

// Added Loop
loop ::= `(` `while` expression statement `)`
assign ::= `()` `=` var expression `)`
statement::= vardec | loop | assign
//End Loop

op ::= `x` | `-`|  `&&` | `||`
program ::= vardec*

// * means zero or more of the word
// Other form: program ::= epsilon (empty) | vardec program

````

Using the Grammar

````
(vardec int x)
(vardec bool y true)
(vardec int a (+1 2))

//With loop
(vardec int x 0)
(while (< x 10) (= x ( + x 1)))



````

Java Grammar

````
int x  = 7;
boolean y = true;
int a = 1+2;
boolean b = false && true;

//With Loop
int x = 0;
while (x < 10){
  x = x + 1;
}

````

- This Grammar is not Turing Complete; cannot do iteration. Unless, loop is stated
- Iterative process in design
- Current Target Language is JavaScript.


#### Terms in Compilers

- Object Lang: The designed language
- MetaLanguage: The language which the compiler is written in
- Target Language: The language which our compiler compiles to



#### Library 

- Jacoco
  - Reporting that code 
- Junit
  - Testing that code

