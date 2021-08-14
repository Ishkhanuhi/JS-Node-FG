# JS Loops

Loops offer a quick and easy way to do something repeatedly.  
There are many different kinds of loops, but they all essentially do the same thing:  
they repeat an action some number of times. (Note that it's possible that number could be zero!)

The various loop mechanisms offer different ways to determine the start and end points of the loop.  
There are various situations that are more easily served by one type of loop over the others.  

The statements for loops provided in JavaScript are:  
- `for` statement
- `do...while` statement
- `while` statement
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
  statement_1
  statement_2
      ...
  statement_n
}
```
![test](https://upload.wikimedia.org/wikipedia/commons/0/06/For-loop-diagram.png)  

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

   
