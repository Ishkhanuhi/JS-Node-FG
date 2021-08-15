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
