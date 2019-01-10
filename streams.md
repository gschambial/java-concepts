# Streams

- ## Terminal Operations
  - Terminal operations are either void or return a non-stream result.
  - `filter`, `map`, `sorted`

- ## Intermediate Operations
  - Intermediate operations return a stream so we can chain multiple intermediate operations without using semicolons.
  - `forEach`
 
Most stream operations accept some kind of lambda expression parameter, a functional interface specifying the exact behavior of the operation. Most of those operations must be both non-interfering and stateless. What does that mean?

- A function is **non-interfering** when it does not modify the underlying data source of the stream, e.g. in the above example no lambda expression does modify myList by adding or removing elements from the collection.

- A function is **stateless** when the execution of the operation is deterministic, e.g. in the above example no lambda expression depends on any mutable variables or states from the outer scope which might change during execution.

## Creating Streams

  - `Collection.stream()` or `Collection.parallelStream()`
  - `Stream.of()`
 
## Primitive VS Regular Streams

- Java 8 ships with special kinds of streams for working with the primitive data types `int`, `long` and `double`. As you might have guessed it's `IntStream`, `LongStream` and `DoubleStream`
- `IntStreams` can replace the regular for-loop utilizing `IntStream.range()`

```
IntStream.range(1, 4)
    .forEach(System.out::println);
```
- Primitive streams use specialized lambda expressions, e.g. `IntFunction` instead of `Function` or `IntPredicate` instead of `Predicate`
- Primitive streams support the additional terminal aggregate operations `sum()` and `average()`
- Sometimes it's useful to transform a regular object stream to a primitive stream or vice versa. For that purpose object streams support the special mapping operations `mapToInt()`, `mapToLong()` and `mapToDouble`
```
Stream.of("a1", "a2", "a3")
    .map(s -> s.substring(1))
    .mapToInt(Integer::parseInt)
    .max()
    .ifPresent(System.out::println);
```
- Primitive streams can be transformed to object streams via `mapToObj()`
```
IntStream.range(1, 4)
    .mapToObj(i -> "a" + i)
    .forEach(System.out::println);
```
## Laziness of Intermediate Operations

- An important characteristic of intermediate operations is laziness. Look at this sample where a terminal operation is missing:

```
Stream.of("d2", "a2", "b1", "b3", "c")
    .filter(s -> {
        System.out.println("filter: " + s);
        return true;
    });
```
- When executing this code snippet, nothing is printed to the console. That is because intermediate operations will only be executed when a terminal operation is present.

## Processing Order

- Chained Intermediate operations execute vertically i.e. one element goes throung entire chain instead of entire stream being executed by one intermediate operation after another.

## Reusing Streams

- Java 8 streams cannot be reused. As soon as you call any terminal operation the stream is closed:
```
Stream<String> stream =
    Stream.of("d2", "a2", "b1", "b3", "c")
        .filter(s -> s.startsWith("a"));

stream.anyMatch(s -> true);    // ok
stream.noneMatch(s -> true);   // exception
```
- To overcome this limitation we have to to create a new stream chain for every terminal operation we want to execute, e.g. we could create a stream supplier to construct a new stream with all intermediate operations already set up:
```
Supplier<Stream<String>> streamSupplier =
    () -> Stream.of("d2", "a2", "b1", "b3", "c")
            .filter(s -> s.startsWith("a"));

streamSupplier.get().anyMatch(s -> true);   // ok
streamSupplier.get().noneMatch(s -> true);  // ok
```

