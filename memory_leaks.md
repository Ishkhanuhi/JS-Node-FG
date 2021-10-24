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

Global variables are always available from the root and will never get garbage collected.  
Some mistakes cause variables leak from the local scope into the global scope when in non-strict mode:  
 * assigning value to the undeclared variable,
