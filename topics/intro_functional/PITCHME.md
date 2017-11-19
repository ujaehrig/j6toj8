### Function Programming

- No side effects |
- Functions are values |
- Higher Order Functions |
- Pure Functions |
- Lambda and Closures |
- map, reduce, filter |

+++

### Higher Order Function

- At least one of: |
- Take one ore more function argument |
- Return a function |

- Composition |
- Currying |

Note:
- Composition composes multiple functions 
  to a new function
- Currying modifies function with > 1 arg
  to functions with only one arg which 
  returns a HOF 

+++

### Pure Functions

- Return same output when given the same input |
- No side effect |
- doesn't modify arguments |
- easy to test |
- easy to parallelize |

+++

### Pure or unpure?

- Math.sin() |
- Random.nextInt() |
- List.sort(Comparator)
- Accessor (Getter) |

+++

### Lambda 

TODO

+++

### Closure 

TODO

+++ 

### Map / Reduce / Filter

- doesn't modify input collection |
- map: similar collection with modified elements |
- reduce: one value for collection |
- filter: collection without filtered elements |  

+++

### Map 

```java
Collection<T> result = new Collection<>();
for(Element e :collection) {
    result.add(convert(e));
}
return result;
```

+++

### Reduce 

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

### Filter

```java
Collection<T> result = new Collection<>();
for(Element e : collection) {
    if(filterCondition(e)) {
        result.add(e);
    }
}
return result;
```




