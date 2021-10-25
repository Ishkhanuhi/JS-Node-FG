# Memory leaks in JS

In order to understand memory leaks, at first, we need to understand how memory is managed in JS.  
Here is source to understand memory management in V8 engine: [Visualizing memory management in V8 Engine](https://dev.to/deepu105/visualizing-memory-management-in-v8-engine-javascript-nodejs-deno-webassembly-105p)

During this meeting, we'll cover the following topics:
- What is a memory leak?
- Sources of memory leaks in JS.
  * Accidental global variables
  * Closures
  * Timers
  * Event listeners
  * ...

## What Is a Memory Leak and How to Spot It?

At first, let's define some concepts, which we'll use during this topic.
- **Garbage Collector** 
  Garbage Collector is a background process in the JavaScript engine that identifies unreachable objects,  
  removes them, and reclaims the underlying memory.

- **Stack**
  This is where static data, including method/function frames, primitive values, and pointers to objects are stored.  
  This space is managed by the operating system (OS).  

- **Heap**
  This is where V8 stores objects or dynamic data.  
  This is the biggest block of memory area and it’s where Garbage Collection(GC) takes place.

V8 manages the heap memory through garbage collection.  
In simple terms, it frees the memory used by orphan objects, i.e, objects that are no longer referenced from the Stack,  
directly or indirectly (via a reference in another object), to make space for new object creation.
The garbage collector in V8 is responsible for reclaiming unused memory for reuse by the V8 process. V8 garbage collectors are generational (Objects in Heap are grouped by their age and cleared at different stages). There are two stages and three different algorithms used for garbage collection by V8.

In simple terms, a memory leak is nothing but an orphan block of memory on the heap that is no longer used by the application  
and hasn’t been returned to the OS by the garbage collector. So in effect, it’s a useless block of memory.  
An accumulation of such blocks over time could lead to the application not having enough memory to work with or  
even your OS not having enough memory to allocate, leading to slowdowns and/or crashing of the application or even the OS.

*An example of a reference chain from a Garbage Collector root to the objects*
![](https://static.ditdot.hr/images/dev/010/reference-chain-garbage-collector.png)  


*Object 4 is not reachable and will be removed from the memory.  
Object 3 is still reachable through the forgotten reference from Object 2 and will not be garbage collected.*  

![](https://static.ditdot.hr/images/dev/010/reference-chain-memory-leaks.png)

How to figure out that our code is leaking memory? Well, memory leaks are sneaky and often difficult to notice and to localize.  
The leaking JavaScript code is not in any way considered invalid, and the browser will not throw any error while running it.  
If we notice that our page's performance is getting progressively worse, the browser's built-in tools can help us determine if a memory leak exists and what objects cause it.  

## Common Sources of Memory Leaks in JavaScript Code

The following is a helpful list of places in code that are more susceptible to memory leaks  
and deserve special consideration when managing the memory.  

### Accidental global variables

Since global variables in JavaScript are referenced by the root node (window or global `this`),  
they are never garbage collected throughout the lifetime of the application, and will occupy memory as long as the application is running.  
This applies to any object referenced by the global variables and all their children as well.  
Having a large graph of objects referenced from the root can lead to a memory leak.

When you assign a value to an undeclared variable, JavaScript automatically hoists it as a global variable in default mode.  
This could be the result of a typo and could lead to a memory leak.  
Another way could be when assigning a variable to `this`, which is still a holy grail in JavaScript.  
```
function createGlobalVariables() {
  leaking1 = 'I leak into the global scope'; // assigning value to the undeclared variable
  this.leaking2 = 'I also leak into the global scope'; // 'this' points to the global object
};
createGlobalVariables();
window.leaking1; // 'I leak into the global scope'
window.leaking2; // 'I also leak into the global scope'
```

When you use arrow functions, you also need to be mindful not to create accidental globals, and unfortunately,  
strict mode will not help with this. You can use the `no-invalid-this` rule from ESLint to avoid such cases.  
If you are not using ESLint, just make sure not to assign to this from global arrow functions.  

```
// This will also become a global variable as arrow functions
// do not have a contextual `this` and instead use a lexical `this`
const hello = () => {
    this.foo = 'Message";
}
```
### Use Global Scope Sparingly
 * As much as possible, don’t use the global scope.  
   Instead, use local scope inside functions, as those will be garbage collected and memory will be freed.  
   If you have to use a global variable due to some constraints, set the value to `null` when it’s no longer needed.
 * Use global variables only for example, constants, cache.  
   Don’t use global variables for the convenience of avoiding passing values around.  
   For sharing data between functions and classes, pass the values around as parameters or object attributes.
 * Don’t store big objects in the global scope. If you have to store them, make sure to nullify them when they are not needed.  
   For cache objects, set a handler to clean them up once in a while and don’t let them grow indefinitely.

### USE STACK MEMORY EFFECTIVELY

 * Avoid heap object references from stack variables when possible. Also, don’t keep unused variables.
 * Destructure and use fields needed from an object or array rather than passing around entire objects/arrays to functions,  
   closures, timers, and event handlers. This avoids keeping a reference to objects inside closures.  
   The fields passed might mostly be primitives, which will be kept in the stack.
 ```
 function outer() {
    const obj = {
        foo: 1,
        bar: "hello",
    };

    const closure = () {
        const { foo } = obj;
        myFunc(foo);
    }
}

function myFunc(foo) {}
```
### USE HEAP MEMORY EFFECTIVELY

It’s not possible to avoid using heap memory in any realistic application,  
but we can make them more efficient by following some of these tips:

* Copy objects where possible instead of passing references.
* Pass a reference only if the object is huge and a copy operation is expensive.
* Avoid object mutations as much as possible. Instead, use object spread or Object.assign to copy them.
* Avoid creating multiple references to the same object. Instead, make a copy of the object.
* Use short-lived variables.
* Avoid creating huge object trees. If they are unavoidable, try to keep them short-lived in the local scope.
