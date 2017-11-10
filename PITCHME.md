# Java 6 to Java 8 
## What changed?

+++

### Overview

- Java 7 Goodies |
- Functional Interfaces |
- Default Methods |
- Lambda Expressions |

+++

### Overview cont'd

- Method References |
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

- Package: java.util.function |
- Predicate |
- Consumer |
- Supplier |
- Function |

Note:
- Predicate returns boolean, accepts 1 argument
- BiPredicate and native variants
- HOF Predicate: and, or, negate
- Consumer returns void and accepts 1 argument
- BiConsumer and native variants
- HOF Consumer: andThen
- Supplier returns a type and accepts nothing
- native variants
- Function returns type R, accepts type T
- BiFunction, Operator and native variants
- HOF Function: compose, andThen

---

### Default Methods

- Allows code in interfaces |
- Backward compatibility for interfaces |

Note:
- HOF as default methods

---

### Lambda Expressions

- Uses functional interfaces |
- Closure (function + environment) |
- Replacement for some anonymous classes |
- but consider the scope! |
- Syntax: (params) -> code |
- Can be used as variable |

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
- Use parameter type inference |
- Omit parentheses on single arguments |
- Keep lambda expressions short |

Note:
- @FunctionalInterface seems superfluous, but will check, if interface has only one method
- default methods might clash
- In most cases the type can be inferred and should not be written in the parameter list
- Without parentheses the code looks cleaner 
- Think of Lambda as expression

+++

### Best practices

- Avoid blocks |
- Avoid return statements |
- Avoid side effects |
- Prefer method references |

Note:
- Like before: Keep lambda short
- return is allowed, but usually unnecessary on one-liners
- Methods references are better readable

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

i -> i.toString()
Integer::toString

x -> System.out.println(x)
System.out::println
```
@[1-2](static method)
@[4-5](constructor)
@[7-8](instance method)
@[10-11](instance method of object)


---

### Optional

- Replacement for null returns |
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
- Prefer empty Collection to Optional&lt;Collection> |
- Don't use for fields |
- Don't use for parameters |
- Prefer orElse() to get() |
- Consider Null object pattern |

Note:
- Optional is not serializable (fields)
- Unncessary wrapping (parameters)
- get() might throw
- http://dolszewski.com/java/java-8-optional-use-cases/

---

### Stream API

- Package: java.util.stream |
- Stream and native Variants |
- intermediate methods |
- terminal methods |
- Spliterator, serial vs. parallel |
- Collectors, StreamSupport |

Note:
- Stream, DoubleStream, etc and StreamSupport
- intermediate methods return a stream
- terminal methods return void
- Spliterator: traverse and partition

+++

### Intermediate 

- map(Function&lt;T, R>) |
- filter(Predicate&lt;T>) |
- flatMap(Function&lt;T, Stream&lt;R>>) |
- distinct() |
- sorted() |

+++

### Terminal

- reduce() |
- collect() |
- use Collectors class |
- allMatch(), anyMatch() |
- min(), max(), count() |

+++

### Examples

```java
List<Integer> list;

list.stream().map(Integer::toString).collect(Collectors.toList());
list.stream().filter(i -> i > 0).collect(Collectors.toList());
list.stream().distinct().collect(Collectors.toList());
list.stream().sorted().collect(Collectors.toList());
```
@[3](map an int to a string)
@[4](filter all ints > 0)
@[5](remove duplicates)
@[6](sort the stream)

+++

### Exercise

Find the longest line in a file

- Files.lines(Path) |
- Comparator.comparingInt(ToIntFunction<? super T>) |
- Stream.max(Comparator<? super T>) |
- BaseStream.close() |

Note:
- Files.lines returns lines of a text file
- comparingInt returns a Comparator with a given function
- Stream#max returns the max element for a given Comparator
- BaseStream@close is needed for InputStreams etc.

+++

### Solution

```java
try(Stream<String> lines = Files.lines(path)) {
    final Optional<String> max = 
       lines.max(Comparator.comparingInt(String::length));
    String maxString = max.get();
    System.out.println(maxString.length() + " : " + maxString);
}
```

---

### Date-Time API

- Package: java.time |
- Replaces Joda-Time |
- Immutable types |
- Clock and Instant |
- Duration vs. Period |
- LocalDateTime vs. ZonedDateTime vs. OffsetDateTime |

Note:
- Instead of ms since 1st Jan '70, it's now seconds and ns 
- LocalDateTime can't represent an Instant w/o timezone
- Duration is time-based, Period is date-based

---

### Useful Links

- https://blog.idrsolutions.com/2014/10/5-minutes-explanation-java-lambda-expression/
- https://blog.idrsolutions.com/2014/11/java-8-streams-explained-5-minutes/
- https://blog.idrsolutions.com/2015/01/java-8-default-methods-explained-5-minutes/
- https://blog.idrsolutions.com/2015/02/java-8-method-references-explained-5-minutes/
- https://blog.idrsolutions.com/2015/04/java-8-optional-class-explained-in-5-minutes/
