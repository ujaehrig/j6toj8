### Functional Programming

- No side effects |
- Functions are values |
- Higher Order Functions |
- Pure Functions |
- Lambda and Closures |
- map, reduce, filter |

+++

### Functions are values

- Functions can be assigned to variables |
- Functions are first-class citizen |

+++

### Higher Order Functions

- At least one of these two: |
- Take one ore more function argument |
- Return a function |

- Composition, Currying |

Note:
- Composition composes multiple functions 
  to a new function
- Currying modifies function with > 1 arg
  to functions with only one arg which 
  returns a HOF. 
  Example: divide(x, y): return x/y
   => div(d): return x -> divide(x, d) 

+++

### Pure Functions

- Return same output when given the same input |
- No side effect |
- don't modify arguments |
- easy to test |
- easy to parallelize |

+++

### Pure or unpure?

- Math.sin() |
- Random.nextInt() |
- List.sort(Comparator) |
- Accessor (Getter) |

+++

### Lambda 

- Lambda calculus (mathematics) | 
- Anonymous function |
- Can have closure (later) |
- Not recursive |

+++

### Closure (function closure)

- Bound variables |
- function scope vs. outer scope |
- function + variables |
- Java: final / effective final | 

Note:
The variables outside the function scope
must be final or effective final and can't
be changed. 

+++ 

### Map / Reduce / Filter

- don't modify input collection |
- map: similar collection with modified elements |
- reduce: one value for collection |
- filter: collection without filtered elements |  

+++

### Map similar to

```java
Collection<T> result = new Collection<>();
for(Element e :collection) {
    result.add(convert(e));
}
return result;
```

+++

### Reduce similar to

```java
T result = identity;
for(T e : collection) {
    result = accumulator(result, e);
}
return result;
```

Note:
- identity must be identity for accumulator
  i.e. accumulator(identity, u) == u
- accumulator must be associative 
  (a * b) * c == a * (b * c)

+++

### Filter similar to

```java
Collection<T> result = new Collection<>();
for(Element e : collection) {
    if(filterCondition(e)) {
        result.add(e);
    }
}
return result;
```

