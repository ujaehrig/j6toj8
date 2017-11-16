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
