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

At first, let's define a concept, which we'll use during this topic.
- **Garbage Collector** 
  Garbage Collector is a background process in the JavaScript engine that identifies unreachable objects,  
  removes them, and reclaims the underlying memory.

A memory leak occurs when an object in memory that is supposed to be cleaned in a garbage collection cycle,  
stays reachable from the root through an unintentional reference by another object.  
Keeping redundant objects in memory results in excessive memory use inside the app and can lead to degraded and poor performance.  

[tesr](https://www.ditdot.hr/en/causes-of-memory-leaks-in-javascript-and-how-to-avoid-them)  
