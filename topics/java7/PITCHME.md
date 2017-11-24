### Java 7 Goodies

- try with resource |
- Diamond operator |
- Multi Catch |
- string switch |
- java.io.file API |

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
