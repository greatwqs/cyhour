---
layout: post
title: "Using Mockito's @InjectMocks"
---

> FYI: Like the [previous post]({% post_url 2015-02-19-dump-postgres-table-inserts %}),
> this is a really quick tip.

Let's imagine we have two classes, and one depends on another:

### Another.java:

```java
@Log
public class Another {
    public final void doSomething() {
        log.info("another service is working...");
    }
}
```

### One.java:

```java
@Log
@RequiredArgsConstructor
public class One {
    private final transient Another another;

    public final void work() {
        log.info("Some service is working");
        another.doSomething();
        log.info("Worked!");
    }
}
```

Now, if we want to test `One`, we need an instance of `Another`. While we
are testing `One`, we don't really care about `Another`, so, we use a
Mock instead.

In Java world, it's pretty common to use Mockito for such cases. A common
approach would be something like this:

### OneTest.java:
```java
public final class OneTest {
    @Mock
    private transient Another another;
    private transient One one;

    @Before
    public void setup() {
        MockitoAnnotations.initMocks(this);
        this.one = new One(another);
    }

    @Test
    public void oneCanWork() throws Exception {
        one.work();
        Mockito.verify(another).doSomething();
    }
}
```

It works, but it's unnecessary to call the `One` constructor by hand, we can
just use [`@InjectMocks`][javadoc] instead:

### OneTest.java (2):

```java
public final class OneTest {
    @Mock
    private transient Another another;
    @InjectMocks
    private transient One one;

    @Before
    public void setup() {
        MockitoAnnotations.initMocks(this);
    }

    @Test
    public void oneCanWork() throws Exception {
        one.work();
        Mockito.verify(another).doSomething();
    }
}
```

It does have some limitations, but for most cases it will work gracefully.

If feel like more info, read the [Javadoc][javadoc] for it.

[javadoc]: http://site.mockito.org/mockito/docs/current/org/mockito/InjectMocks.html
