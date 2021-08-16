# JS Loops

Loops offer a quick and easy way to do something repeatedly.  
There are many different kinds of loops, but they all essentially do the same thing:  
they repeat an action some number of times. (Note that it's possible that number could be zero!)

The various loop mechanisms offer different ways to determine the start and end points of the loop.  
There are various situations that are more easily served by one type of loop over the others.  

The statements for loops provided in JavaScript are:  
- `for` statement
- `while` statement
- `do...while` statement
- `labeled` statement
- `break` statement
- `continue` statement
- `for...in` statement
- `for...of` statement

## `for` statement
A `for` loop repeats until a specified condition evaluates to `false`.  
The JavaScript `for` loop is similar to the Java and C `for` loop.

A `for` statement looks as follows:
```
for ([initialExpression]; [conditionExpression]; [finalExpression]) {
  statement_1;
  statement_2;
      ...
  statement_n;
}
```
![](https://upload.wikimedia.org/wikipedia/commons/0/06/For-loop-diagram.png)  

When a `for` loop executes, the following occurs:
1. The initializing expression `initialExpression`, if any, is executed.  
   This expression usually initializes one or more loop counters, but the syntax allows an expression of any degree of complexity.  
   This expression may optionally declare new variables with `var` or `let` keywords.  
   Variables declared with `var` are **not** local to the loop, i.e. they are in the same scope the `for` loop is in.  
   Variables declared with `let` are local to the statement.  
   **Note:** This step is executed first, and only once and you are not required to put a statement here, as long as a semicolon appears.  
   
2. The `conditionExpression` expression is evaluated.  
   If the value of `conditionExpression` is `true`, the loop statements execute.  
   If the value of condition is `false`, the `for` loop terminates.  
   (If the condition expression is omitted entirely, the condition is assumed to be `true`.)
3. The `statement_1`, `statement_2`, ... `statement_n` execute.  
   In case of only one `statement`, the `{...}` (curly braces) can be omitted.
4. If present, the update expression `finalExpression` is executed.  
   An expression to be evaluated at the end of each loop iteration.  
   This occurs before the next evaluation of `conditionExpression`.  
   Generally used to update or increment the counter variable.
5. Control returns to Step 2.

   ```
   for (let i = 0; i < 9; ++i) {
      console.log(i);
      // more statements
   }
   ***
   let i = 0;
   for (; i < 9; ++i) {
      console.log(i);
      // more statements
   }
   ***
   for (let i = 0;; ++i) {
      console.log(i);
      if (i > 3) break;
      // more statements
   }
   ***
   let i = 0;
   for (;;) {
      if (i > 3) break;
      console.log(i);
      ++i;
   }
   ```
   
## `while` statement
   The `while` statement creates a loop that executes a specified statement as long as the test condition evaluates to `true`.  
   The `condition` is evaluated before executing the statement.  
   A `while` statement looks as follows:  
   ```
   while (condition) {
      statement_1;
      statement_2;
          ...
      statement_n;
   }
   ```  
   ![](https://snappygoat.com/b/82a0c0dbd1b1b048d4e0c52c2935d10a8dfe934b)  
   - `condition`
      An expression evaluated before each pass through the loop.  
      If this `condition` evaluates to `true`, `statement_1`, `statement_2`, ... `statement_n` are executed.  
      When `condition` evaluates to `false`, execution continues with the statement after the `while` loop.
   - `statement_i, i = 1, 2, ..., n`
      The sequence of statements is executed if and only if the `condition` is evaluated to `true`.  
      In case of only one `statement`, the `{...}` (curly braces) can be omitted.  
   
   ```
   let n = 0;
   let x = 0;

   while (n < 3) {
      ++n;
      x += n;
   }
   ```
   
   
## `do...while` statement
   The `do...while` statement creates a loop that executes a specified statement until the test condition evaluates to false.  
   The condition is evaluated after executing the statement, resulting in the specified statement executing at least once.  
   
   A `do...while` statement looks as follows:
   ```
   do {
     statement_1;
     statement_2;
        ...
     statement_n;
   }
   while (condition);
   ```  
   ![](https://snappygoat.com/b/a0e6be5183f4fe123c1e8c86a4912ddaa341186b)  
   
- `statement_i, i = 1, 2, ..., n`  
    A sequence of statements or a statement that is executed at least once and is re-executed each time the condition evaluates to `true`. In case of only one `statement`, the `{...}` (curly braces) can be omitted.  
- If `condition` is `true`, the `statement` executes again. At the end of every execution, the condition is checked. When the condition is false, execution stops, and control passes to the statement following do...while.
   
   ```
   let result = '';
   var i = 0;
   do {
      i += 1;
      result += i + ' ';
   }
   while (i > 0 && i < 5);
      // Despite i == 0 this will still loop as it starts off without the test
      console.log(result);
   ```

## Differences between `do...while` and `while` statements
| **While Loop**  | **Do...while loop**  |
|---|---|
| This is entry controlled loop. It checks condition before entering into loop.  |  This is exit control loop. Checks condition when coming out from loop. |
|  The `while` loop may run zero or more times. | 	`do...while` may run more than one time but at least once.  |
| The variable of test condition must be initialized prior to entering into the loop.  |  The variable for loop condition may also be initialized in the loop also. |


## `labeled` statement
A `label` provides a statement with an identifier that lets you refer to it elsewhere in your program.  
For example, you can use a `label` to identify a loop, and then use the `break` or `continue` statements  
to indicate whether a program should interrupt the loop or continue its execution.  

The syntax of the labeled statement looks like the following:
```
label:
  statement
```
- `label`
   Any JavaScript identifier that is not a reserved word.  
- `statement`
   A JavaScript statement. `break` can be used with any labeled statement, and `continue` can be used with looping labeled statements.

**Note:** JavaScript has **NO** `goto` statement, you can only use labels with `break` or `continue`.  
In strict mode code, you can't use "let" as a label name. It will throw a SyntaxError (let is a reserved identifier).

### Using a labeled continue with for loops
```
let i, j;

loop1:
for (i = 0; i < 3; i++) {      //The first for statement is labeled "loop1"
   loop2:
   for (j = 0; j < 3; j++) {   //The second for statement is labeled "loop2"
      if (i === 1 && j === 1) {
         continue loop1;
      }
      console.log('i = ' + i + ', j = ' + j);
   }
}

// Output is:
//   "i = 0, j = 0"
//   "i = 0, j = 1"
//   "i = 0, j = 2"
//   "i = 1, j = 0"
//   "i = 2, j = 0"
//   "i = 2, j = 1"
//   "i = 2, j = 2"
// Notice how it skips both "i = 1, j = 1" and "i = 1, j = 2"
```

### Using a labeled break with for loops
```
let i, j;

loop1:
for (i = 0; i < 3; i++) {      //The first for statement is labeled "loop1"
   loop2:
   for (j = 0; j < 3; j++) {   //The second for statement is labeled "loop2"
      if (i === 1 && j === 1) {
         break loop1;
      }
      console.log('i = ' + i + ', j = ' + j);
   }
}

// Output is:
//   "i = 0, j = 0"
//   "i = 0, j = 1"
//   "i = 0, j = 2"
//   "i = 1, j = 0"
// Notice the difference with the previous continue example
```

### Using a labeled block with break
```
foo: {
  console.log('This line will be executed at first.');
  break foo;
  console.log('this will not be executed');
}
console.log('Then this line will be executed.');

// this will log:

// 'This line will be executed at first.'
// 'Then this line will be executed.' 
```
### Labeled function declarations

Starting with ECMAScript 2015, labeled function declarations are standardized for non-strict code:
```
L: function F() {}
```
In strict mode code, however, this will throw a `SyntaxError`:
```
'use strict';

L: function F() {}
// SyntaxError: functions cannot be labelled
```
Generator functions can neither be labeled in strict code, nor in non-strict code:
```
L: function* F() {}
// SyntaxError: generator functions cannot be labelled
```

## `break` statement
The `break` statement terminates the current loop, `switch`, or `label` statement and transfers program control to the statement following the terminated statement.

The syntax of the break statement looks like this:
```
break;
break [label];
```
`label` *Optional*  
Identifier associated with the label of the statement. If the statement is not a loop or switch, this is required.

1. The first form of the syntax terminates the innermost enclosing loop or switch.
2. The second form of the syntax terminates the specified enclosing labeled statement.  

### `break` in `while` loop
```
function testBreak(x) {
  var i = 0;

  while (i < 6) {
    if (i == 3) {
      break;
    }
    i += 1;
  }

  return i * x;
}
```
### `break` in `switch` statements
```
const focusGroup = "node";

switch (focusGroup) {
  case "node":
    console.log("Node Focus Group");
    break;
  case "react":
    console.log("React Focus Group");
    break;
  default:
    console.log("No such Focus Group");
    break;
}
```

### `break` in labeled blocks
```
outer_block: {
  inner_block: {
    console.log('1');
    break outer_block; // breaks out of both inner_block and outer_block
    console.log(':-('); // skipped
  }
  console.log('2'); // skipped
}
```

### `break` in labeled blocks that throw
The following code also uses `break` statements with labeled blocks, but generates a `SyntaxError`.  
A `break` statement must always be nested within any label it references.

```
block_1: {
  console.log('1');
  break block_2; // SyntaxError: label not found
}

block_2: {
  console.log('2');
}
```

### `break` within functions
```
function testBreak(x) {
  var i = 0;

  while (i < 6) {
    if (i == 3) {
      (function() {
        break;
      })();
    }
    i += 1;
  }

return i * x;
}

testBreak(1); // SyntaxError: Illegal break statement
```
```
block_1: {
  console.log('1');
  ( function() {
    break block_1; // SyntaxError: Undefined label 'block_1'
  })();
}
```

## `continue` statement
The `continue` statement terminates execution of the statements in the current iteration of the current or labeled loop,  
and continues execution of the loop with the next iteration.

The syntax of the `continue` statement looks like this:  
`continue [label];`

`label` *Optional*  
Identifier associated with the label of the statement.  
- When you use `continue` without a `label`, it terminates the current iteration of the innermost enclosing `while`,  
  `do-while`, or `for` statement and continues execution of the loop with the next iteration.  
  In contrast to the `break` statement, `continue` does not terminate the execution of the loop entirely.  
  In a `while` loop, it jumps back to the condition. In a `for` loop, it jumps to the increment-expression.
- When you use `continue` with a label, it applies to the looping statement identified with that label.

### Using `continue` with a `label`
```
let i = 0;
let j = 8;

check_i_and_j: while (i < 4) {
  console.log('i: ' + i);
  i += 1;

  check_j: while (j > 4) {
    console.log('j: ' + j);
    j -= 1;

    if ((j % 2) == 0)
      continue check_j;
    console.log(j + ' is odd.');
  }
  console.log('i = ' + i);
  console.log('j = ' + j);
}

//Output:
i: 0

// start checkj
j: 8
7 is odd.
j: 7
j: 6
5 is odd.
j: 5
// end checkj

i = 1
j = 4

i: 1
i = 2
j = 4

i: 2
i = 3
j = 4

i: 3
i = 4
j = 4
```

## `for...in` statement
The `for...in` statement iterates over all enumerable properties of an object that are keyed by strings (ignoring ones keyed by Symbols),  
including inherited enumerable properties.
 A `for...in` statement looks as follows:  
 ```
 for (variable in object)
    statement
 ```
 - `variable`
    A different property name is assigned to `variable` on each iteration.
 - `object`
    Object whose non-Symbol enumerable properties are iterated over.

A `for...in` loop iterates over the properties of an object in an arbitrary order  
(this is why one cannot depend on the seeming orderliness of iteration).  
If a property is modified in one iteration and then visited at a later time, its value in the loop is its value at that later time.  
A property that is deleted before it has been visited will not be visited later.  
Properties added to the object over which iteration is occurring may either be visited or omitted from iteration.

In general, it is best not to add, modify, or remove properties from the object during iteration,  
other than the property currently being visited. There is no guarantee whether an added property will be visited,  
whether a modified property (other than the current one) will be visited before or after it is modified,  
or whether a deleted property will be visited before it is deleted.

```
var obj = {a: 1, b: 2, c: 3};

for (const prop in obj) {
  console.log(`obj.${prop} = ${obj[prop]}`);
}

// Output:
// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```
**Note:** `for...in` should not be used to iterate over an Array where the index order is important.  
Array indexes are just enumerable properties with integer names and are otherwise identical to general object properties.  
There is no guarantee that `for...in` will return the indexes in any particular order.  
The `for...in` loop statement will return all enumerable properties, including those with non–integer names and those that are inherited.

Because the order of iteration is implementation-dependent, iterating over an array may not visit elements in a consistent order.  
Therefore, it is better to use a `for` loop with a numeric index (or `Array.prototype.forEach()` or the `for...of` loop)  
when iterating over arrays where the order of access is important.  

### Iterating own properties
```
var triangle = {a: 1, b: 2, c: 3};

function ColoredTriangle() {
  this.color = 'red';
}

ColoredTriangle.prototype = triangle;

var obj = new ColoredTriangle();

for (const prop in obj) {
  if (obj.hasOwnProperty(prop)) {
    console.log(`obj.${prop} = ${obj[prop]}`);
  }
}

// Output:
// "obj.color = red"
```

## `for...of` statement
The `for...of` statement creates a loop Iterating over iterable objects (including `Array`, `Map`, `Set`, `String`, `arguments` and so on).  
A `for...of` statement looks as follows:  
```
for (variable of iterable) {
  statement
}
```  
`variable`  
On each iteration a value of a different property is assigned to `variable`. `variable` may be declared with `const`, `let`, or `var`.  
`iterable`  
Object whose iterable properties are iterated.

### Iterating over an Array

```
const iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}
// 10
// 20
// 30
```
### Iterating over a String
```
const iterable = 'NODE';

for (const value of iterable) {
  console.log(value);
}
// "N"
// "O"
// "D"
// "E"
```
### Iterating over a Map
```
const iterable = new Map([['a', 1], ['b', 2], ['c', 3]]);

for (const entry of iterable) {
  console.log(entry);
}
// ['a', 1]
// ['b', 2]
// ['c', 3]

for (const [key, value] of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```
### Iterating over a Set
```
const iterable = new Set([1, 1, 2, 2, 3, 3]);

for (const value of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

### Iterating over the arguments object
```
(function() {
  for (const argument of arguments) {
    console.log(argument);
  }
})(1, 2, 3);

// 1
// 2
// 3
```

## Differences between `for...of` and `for...in`
Both `for...in` and `for...of` statements iterate over something. The main difference between them is in what they iterate over.  
The `for...in` statement iterates over the enumerable properties of an object, in an arbitrary order.  
The `for...of` statement iterates over values that the iterable object defines to be iterated over.

### Comparison

|   |  `for...in` | `for...of`  |
|---|---|---|
|  **Applies to** | Enumerable Properties  |  Iterable Collections |
|  **Use with Objects?** | Yes  |  No |
| **Use with Arrays?**  |  Yes, but not advised |  Yes |
|  **Use with Strings?** |  Yes, but not advised |  Yes |

```
Object.prototype.objCustom = function() {};
Array.prototype.arrCustom = function() {};

const iterable = [3, 5, 7];
iterable.foo = 'hello';

for (const i in iterable) {
  console.log(i); // logs "0", "1", "2", "foo", "arrCustom", "objCustom"
}

for (const i in iterable) {
  if (iterable.hasOwnProperty(i)) {
    console.log(i); // logs "0", "1", "2", "foo"
  }
}

for (const i of iterable) {
  console.log(i); // logs 3, 5, 7
}
```
# optimization issues, performance issues...
# switch case without break
