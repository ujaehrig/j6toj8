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
- limit() |

Note:
- map transforms a stream of type T to a stream of type R
- flatMap returns a stream of type T into a stream of streams of type R
  thus a new Stream for each element of the original stream is returned
  Example: Matrix: Stream over rows, return stream of each column

+++

### Terminal

- reduce() |
- collect() |
- use Collectors class |
- allMatch(), anyMatch(), noneMatch() |
- findAny(), findFirst() |
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

### Tooling

#### IntelliJ - Java Stream Debugger

![Example](assets/img/example-1.png)

+++?image=assets/img/example-2.png&size=90% auto
 

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
    System.out.println(maxString.length() + ": " + maxString);
}
```
