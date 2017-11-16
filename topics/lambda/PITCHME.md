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
