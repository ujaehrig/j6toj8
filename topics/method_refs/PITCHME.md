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
Object::toString

x -> System.out.println(x)
System.out::println
```
@[1-2](static method)
@[4-5](constructor)
@[7-8](instance method)
@[10-11](instance method of object)
