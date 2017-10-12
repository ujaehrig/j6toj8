# From Java 6 to Java 8 
## What's new?

+++

### Overview

- Java 7 Goodies |
- Functional Interfaces |
- Default Methods |
- Lambda Expressions |
- Method References |

+++

### Overview cont'd

- Optional |
- Stream API |
- Date-Time API |

---

### Java 7 Goodies

- try with resource |
- Diamond operator |
- Multi Catch |

+++

### Examples

#### try with resource 

```java
InputStream in = null;
try {
    in = new FileInputStream("x.txt");
    // do something
} finally {
    if (in != null) {
        in.close();
    }
} 

try(InputStream in = new FileInputStream(x.txt)) {
    // do something
}
```
@[1-9](Java <7 way) 
@[11-13](Java 7+ way)

+++

### Examples

#### Diamond Operator 

```java
List<String> list = new ArrayList<String>()

List<String> list = new ArrayList<>()
```
@[1](Java <7 way) 
@[3](Java 7+ way)

+++

### Examples

#### Multi Catch 

```java
try {
    // some code
} catch(Exception1 exc) {
    // handle Exception
} catch(Exception2 exc) {
    // handle Exception
}

try {
    // some code
} catch(Exception1 | Exception2 exc ) {
    // handle Exception
}
```
@[1-7](Java <7 way) 
@[9-13](Java 7+ way)

---

### Functional Interfaces

- java.util.function |
- Predicate |
- Consumer |
- Supplier |
- Function |

---

### Default Methods

- Allows code in interfaces |

---

### Lambda Expressions

- Uses functional interfaces |
- Closure (function + environment) |
- Replacement for some anonymous classes |
- but consider the scope! |
- Syntax: (params) -> code |

+++

### Example

```java
ExecutorService executorService = Executors.newCachedThreadPool();

executorService.submit(new Runnable() {
    @Override
        public void run() {
            out.println("Anonymous is in thread: " + currentThread());
        }
    });

executorService.submit(() -> out.println("Lambda is in thread: " + currentThread()));
```
@[3-8](with anonymous class)
@[10](with lambda)

+++

### Best practices

- Use @FunctionalInterface on functional interfaces |
- Avoid too many default methods |
- Use parameter inference |
- Omit parentheses on single arguments |
- Keep lambda expressions short |

+++

### Best practices

- Avoid blocks |
- Avoid return statements |
- Avoid side effects |
- Prefer method references |

---

### Method References

- Instead of Lambda |
- to static: Class::staticMethod |
- to constructor: Class::new |
- to instance method: Class::instanceMethod |
- to method of object: object::instanceMethod |

+++

### Examples

```java
i -> Integer.valueOf(i)
Integer::valueOf

i -> new Integer(i)
Integer::new

x -> x.getValue()
X::getValue

x -> System.out.println(x)
System.out::println
```
@[1-2](static method)
@[4-5](constructor)
@[7-8](instance method)
@[10-11](instance method of object)


---

### Optional

- Replacement for null |
- Enhanced Guava Optional |
- Provides useful methods |

+++

### Examples

```java
{
    Optional<Integer> opt = Optional.of(100);

    opt.isPresent();
    opt.filter(i -> i > 10);
    opt.isPresent(System.out::println);
    opt.map(String::toString);
    opt.orElse(0);
    opt.orElseThrow(IllegalArgumentException::new)
}
```
@[4](Simple presence check)
@[5](If present, do additional check)
@[6](If present, do something)
@[7](If present, return mapped element)
@[8](If not present, return default)
@[9](If not present, throw specific exception)

+++

### Best practices

- Use for return values |
- Don't use for fields |
- Don't use for parameters |
- Prefer orElse() to get() |

---

### Stream API



+++ 

### Exercise

Find the longest line in a file

- Files.lines(Path) |
- Comparator.comparingInt(ToIntFunction<? super T>) |
- Stream.max(Comparator<? super T>) |
- BaseStream.close() |

+++

### Solution

```java
try(Stream<String> lines = Files.lines(path)) {
    final Optional<String> max = lines.max(Comparator.comparingInt(String::length));
    String maxString = max.get();
    System.out.println(maxString.length() + " : " + maxString);
}
```

---

### Date-Time API


---

### Useful Links

- https://blog.idrsolutions.com/2014/10/5-minutes-explanation-java-lambda-expression/
- https://blog.idrsolutions.com/2014/11/java-8-streams-explained-5-minutes/
- https://blog.idrsolutions.com/2015/01/java-8-default-methods-explained-5-minutes/
- https://blog.idrsolutions.com/2015/02/java-8-method-references-explained-5-minutes/
- https://blog.idrsolutions.com/2015/04/java-8-optional-class-explained-in-5-minutes/
