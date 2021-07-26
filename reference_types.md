# Reference Types in JS

## Outline
  1. What is Reference Type?  
  2. Differences between reference and primitive types  
  3. Type Coersion in JS
  4. Examples  
  
## 1. What is Reference Type?

  For a given variable if `typeof` operator returns `Object`, then we can say that  
  the given variable is of `Reference Type`.  
  For example, `Array`, `Function`, `Set`, `Map` are reference types.  
  Reference types are mostly used to declare and describe user defined types.

## 2. Differences between reference and primitive types

  The main difference between reference and primitive types is memory allocation mechanism.  
  In case of primitive type, the declared variable holds tha value assigned to it.  
  And, for declared variable, memory is allocated from stack.  
  Let's see what is done when we declare a variable of primitive type.  
  [primitive type memory allocation](https://felixgerschau.com/static/b94165593eb6e02d73039d8b2cfccfdd/c1b63/stack-memory-explained.png)
  
  
  In case of reference types, the declared variables holds not the value, but the reference to allocated memory.  
  [reference type memory allocation](https://felixgerschau.com/static/b452488bd7eeac0405c48f164da6280d/c1b63/stack-heap-pointers.png)
  
 ## 3. Type coersion in JS
  
  Type coercion is the process of converting value from one type to another (such as string to number, object to boolean, and so on).  
  Any type, be it primitive or an object, is a valid subject for type coercion.  
  As an example of type coercion in practice,  
  look at the JavaScript Comparison Table, which shows how the loose equality == operator behaves for different a and b types.  
  [Comparison Table](https://dorey.github.io/JavaScript-Equality-Table)
  
  Type coercion can be explicit and implicit.  
  When a developer expresses the intention to convert between types by writing the appropriate code,  
  like `Number(value)`, it’s called explicit type coercion (or type casting).  
  Since JS is a weakly-typed language, values can also be converted between different types automatically,  
  and it is called implicit type coercion.  
  It usually happens when you apply operators to values of different types, like
  `1 == null`, `2/'5'`, `null + new Date()`, 
  or it can be triggered by the surrounding context, like with `if (value) {…}`, where `value` is coerced to `boolean`.  
  One operator that does not trigger implicit type coercion is `===`, which is called the strict equality operator.
  
  ### Three types of conversion
  The first rule to know is there are only three types of conversion in JavaScript:   
    1. to string  
    2. to number  
    3. to boolean
    
    
    
  ## 4. Examples on Type Coersion
  
  ```
  true + false
  12 / "6"
  "number" + 15 + 3
  15 + 3 + "number"
  [1] > null
  "foo" + + "bar"
  'true' == true
  false == 'false'
  null == ''
  !!"false" == !!"true"
  [‘x’] == ‘x’
  [] + null + 1
  [1,2,3] == [1,2,3]
  {}+[]+{}+[1]
  !+[]+[]+![]
  new Date(0) - 0
  new Date(0) + 0
  ```
  
