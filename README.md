# Monty

This is a repository for the Monty project, which involves creating an interpreter for Monty ByteCode files. Monty is a scripting language that relies on a unique stack with specific instructions to manipulate it.

## Learning Objectives

By the end of this project, you should be able to explain the following concepts without using external references:

### General

- Understanding of LIFO (Last-In, First-Out) and FIFO (First-In, First-Out)
- Knowledge of stacks, their purpose, and when to use them
- Understanding of queues, their purpose, and when to use them
- Familiarity with common implementations of stacks and queues
- Knowledge of common use cases for stacks and queues
- Proper usage of global variables

### Requirements

- Allowed editors: vi, vim, emacs
- Code will be compiled on Ubuntu 20.04 LTS using gcc, with the following options: -Wall -Werror -Wextra -pedantic -std=c89
- All files should end with a new line
- A README.md file at the root of the project folder is mandatory
- Code should follow the Betty style, checked with betty-style.pl and betty-doc.pl
- Maximum of one global variable allowed
- No more than 5 functions per file
- C standard library can be used
- Prototypes of all functions should be included in the header file monty.h
- Pushed header files should be include guarded

## Data Structures

### Stack Structure

```c
/**
 * struct stack_s - doubly linked list representation of a stack (or queue)
 * @n: integer
 * @prev: points to the previous element of the stack (or queue)
 * @next: points to the next element of the stack (or queue)
 *
 * Description: doubly linked list node structure
 * for stack, queues, LIFO, FIFO
 */
typedef struct stack_s
{
    int n;
    struct stack_s *prev;
    struct stack_s *next;
} stack_t;
```

### Instruction Structure

```c
/**
 * struct instruction_s - opcode and its function
 * @opcode: the opcode
 * @f: function to handle the opcode
 *
 * Description: opcode and its function
 * for stack, queues, LIFO, FIFO
 */
typedef struct instruction_s
{
    char *opcode;
    void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;
```

## Compilation & Output

The code will be compiled using the following command:

```
$ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty
```

- All output should be printed on stdout.
- All error messages should be printed on stderr.

# Monty Language

Monty is a scripting language that serves as an interpreter for Monty ByteCodes files. This README provides an overview of the Monty language and instructions on how to use the provided functionalities.

## Monty ByteCode Files

Monty byte code files have the `.m` extension and consist of instructions written in Monty byte codes. Each instruction is written on a separate line and can have any number of spaces before or after the opcode and its argument. Blank lines and additional text after the opcode or its required argument are ignored.

Example of a Monty byte code file (`bytecodes/000.m`):
```
push 0
push 1
push 2
  push 3
                   pall    
push 4
    push 5    
      push    6        
pall
```

## The Monty Program

The Monty program is executed with the following command: `monty file`, where `file` is the path to the Monty byte code file. The program interprets the bytecodes line by line and stops execution if:
- Every line of the file is executed properly
- An error is encountered in the file
- An error occurs during execution

### Error Handling
- If no file or more than one argument is provided, the program displays the error message `USAGE: monty file` and exits with status `EXIT_FAILURE`.
- If the file cannot be opened, the program displays the error message `Error: Can't open file <file>` and exits with status `EXIT_FAILURE`, where `<file>` is the name of the file.
- If an invalid instruction is encountered in the file, the program displays the error message `L<line_number>: unknown instruction <opcode>` and exits with status `EXIT_FAILURE`, where `<line_number>` is the line number where the instruction appears.
- If the program is unable to allocate memory using `malloc`, the program displays the error message `Error: malloc failed` and exits with status `EXIT_FAILURE`.

### Available Functionalities

#### 0. push, pall
- The `push` opcode pushes an element to the stack.
  - Usage: `push <int>` where `<int>` is an integer.
  - If `<int>` is not an integer or no argument is given, the program displays the error message `L<line_number>: usage: push integer` and exits with status `EXIT_FAILURE`, where `<line_number>` is the line number in the file.
- The `pall` opcode prints all the values on the stack, starting from the top of the stack.
  - Usage: `pall`
  - If the stack is empty, nothing is printed.

#### 1. pint
- The `pint` opcode prints the value at the top of the stack, followed by a new line.
  - Usage: `pint`
  - If the stack is empty, the program displays the error message `L<line_number>: can't pint, stack empty` and exits with status `EXIT_FAILURE`.

#### 2. pop
- The `pop` opcode removes the top element of the stack.
  - Usage: `pop`
  - If the stack is empty, the program displays the error message `L<line_number>: can't pop an empty stack` and exits with status `EXIT_FAILURE`.

#### 3. swap
- The `swap` opcode swaps the top two elements of the stack.
  - Usage: `swap`
  - If the stack contains less than two elements, the program displays the error message `L<line_number>: can't swap, stack too short` and exits with status `EXIT_FAILURE`.
# Monty GitHub Repository

This repository contains the source code and implementation for the Monty language. Monty is a simple programming language with a stack-based architecture.

## Table of Contents

1. [Description](#description)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Implemented Opcodes](#implemented-opcodes)
    - [add](#add)
    - [nop](#nop)
    - [sub](#sub)
    - [div](#div)
    - [mul](#mul)
    - [mod](#mod)
    - [comments](#comments)
    - [pchar](#pchar)
    - [pstr](#pstr)
    - [rotl](#rotl)
    - [rotr](#rotr)
    - [stack and queue](#stack-and-queue)
    - [Brainf*ck](#brainfuck)
    - [Add two digits](#add-two-digits)
    - [Multiplication](#multiplication)
    - [Multiplication level up](#multiplication-level-up)

## Description<a name="description"></a>

Monty is a minimalistic, stack-based programming language that supports various opcodes for performing arithmetic operations, manipulating the stack, and executing Brainf*ck scripts. This repository contains the source code for the Monty interpreter.

## Installation<a name="installation"></a>

To use the Monty interpreter, follow these steps:

1. Clone the repository:

   ```
   git clone https://github.com/your-username/monty.git
   ```

2. Change to the `monty` directory:

   ```
   cd monty
   ```

3. Compile the source code:

   ```
   gcc -Wall -Werror -Wextra -pedantic *.c -o monty
   ```

## Usage<a name="usage"></a>

Once you have compiled the Monty interpreter, you can execute Monty programs by running the `monty` executable and passing the path to the Monty bytecode file as an argument:

```
./monty path/to/bytecode_file.m
```

## Implemented Opcodes<a name="implemented-opcodes"></a>

The Monty interpreter supports the following opcodes:

### add<a name="add"></a>

The `add` opcode adds the top two elements of the stack.

Usage: `add`

If the stack contains less than two elements, it prints the error message `L<line_number>: can't add, stack too short`, followed by a new line, and exits with the status `EXIT_FAILURE`.

The result is stored in the second top element of the stack, and the top element is removed.

Example:
```
push 1
push 2
push 3
pall
add
pall
```
Output:
```
3
2
1
5
1
```

### nop

The `nop` opcode does nothing.

Usage: `nop`

### sub

The `sub` opcode subtracts the top element of the stack from the second top element of the stack.

Usage: `sub`

If the stack contains less than two elements, it prints the error message `L<line_number>: can't sub, stack too short`, followed by a new line, and exits with the status `EXIT_FAILURE`.

The result is stored in the second top element of the stack, and the top element is removed.

Example:
```
push 1
push 2
push 10
push 3
sub
pall
```
Output:
```
7
2
1
```

### div

The `div` opcode divides the second top element of the stack

 by the top element of the stack.

Usage: `div`

If the stack contains less than two elements, it prints the error message `L<line_number>: can't div, stack too short`, followed by a new line, and exits with the status `EXIT_FAILURE`.

If the top element of the stack is 0, it prints the error message `L<line_number>: division by zero`, followed by a new line, and exits with the status `EXIT_FAILURE`.

The result is stored in the second top element of the stack, and the top element is removed.

### mul

The `mul` opcode multiplies the second top element of the stack with the top element of the stack.

Usage: `mul`

If the stack contains less than two elements, it prints the error message `L<line_number>: can't mul, stack too short`, followed by a new line, and exits with the status `EXIT_FAILURE`.

The result is stored in the second top element of the stack, and the top element is removed.

### mod

The `mod` opcode computes the remainder of the division of the second top element of the stack by the top element of the stack.

Usage: `mod`

If the stack contains less than two elements, it prints the error message `L<line_number>: can't mod, stack too short`, followed by a new line, and exits with the status `EXIT_FAILURE`.

If the top element of the stack is 0, it prints the error message `L<line_number>: division by zero`, followed by a new line, and exits with the status `EXIT_FAILURE`.

The result is stored in the second top element of the stack, and the top element is removed.

### comments

Lines starting with `#` are treated as comments and are ignored.

### pchar

The `pchar` opcode prints the character at the top of the stack, followed by a new line.

Usage: `pchar`

The integer stored at the top of the stack is treated as the ASCII value of the character to be printed.

If the value is not in the ASCII table, it prints the error message `L<line_number>: can't pchar, value out of range`, followed by a new line, and exits with the status `EXIT_FAILURE`.

If the stack is empty, it prints the error message `L<line_number>: can't pchar, stack empty`, followed by a new line, and exits with the status `EXIT_FAILURE`.

### pstr

The `pstr` opcode prints the string starting at the top of the stack, followed by a new line.

Usage: `pstr`

The integer stored in each element of the stack is treated as the ASCII value of the character to be printed.

The string stops when either:
- The stack is empty
- The value of the element is 0
- The value of the element is not in the ASCII table

If the stack is empty, it prints only a new line.

### rotl

The `rotl` opcode rotates the stack to the top.

Usage: `rotl`

The top element of the stack becomes the last one, and the second top element of the stack becomes the first one.

### rotr

The `rotr` opcode rotates the stack to the bottom.

Usage: `rotr`

The last element of the stack becomes the top element of the stack.

### stack and queue

The `stack` opcode sets the format of the data to a stack (LIFO). This is the default behavior of the program.

Usage: `stack`

The `queue` opcode sets the format of the data to a queue (FIFO).

Usage: `queue`

When switching mode:
- The top of the stack becomes the front of the

 queue.
- The front of the queue becomes the top of the stack.

### Brainf*ck

The `bf/1000-school.bf` file contains a Brainf*ck script that prints "School", followed by a new line.

### Add two digits

The `bf/1001-add.bf` file contains a Brainf*ck script that reads two digits from stdin, adds them, and prints the result.

The total of the two digits will be one digit-long

### Multiplication

The `bf/1002-mul.bf` file contains a Brainf*ck script that reads two digits from stdin, multiplies them, and prints the result.

The result of the multiplication will be one digit-long (<10).

### Multiplication level up

The `bf/1003-mul.bf` file contains a Brainf*ck script that reads two digits from stdin, multiplies them, and prints the result, followed by a new line.

To execute the Brainf*ck scripts, you can use the `bf` interpreter. For example:

```
$ bf bf/1000-school.bf
School
$ bf bf/1001-add.bf
81
9
$ bf bf/1002-mul.bf
24
8
$ bf bf/1003-mul.bf
77
49
```
