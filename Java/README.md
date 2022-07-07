# Java

## Exception with cause

```java
throw new RuntimeException("message", causeException);
```

## Double brace initialisation 

> Double brace initialisation creates an anonymous class derived
> from the specified class (the outer braces), and provides an
> initialiser block within that class (the inner braces). e.g.
> ```java
> new ArrayList<Integer>() {{
>    add(1);
>    add(2);
> }};
> ```
>
> https://stackoverflow.com/a/1958961/14350146

## Static block

> It is also known as a static initializer block or static initialization block in Java
> The code inside the static block body executes once when the class is loaded into the memory.
>
> https://www.delftstack.com/howto/java/static-block-in-java/
