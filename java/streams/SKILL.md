---
name: streams
description: Streams API in Java
---

# Java Streams API

## Crear Streams

```java
// De colecciones
List<String> list = List.of("A", "B", "C");
Stream<String> stream = list.stream();
Stream<String> parallelStream = list.parallelStream();

// De arrays
String[] array = {"A", "B", "C"};
Stream<String> streamFromArray = Arrays.stream(array);
Stream<String> streamFromArray2 = Stream.of("A", "B", "C");

// De valores
Stream<Integer> single = Stream.of(42);
Stream<Integer> empty = Stream.empty();

// De builder
Stream<String> builder = Stream.<String>builder()
    .add("A")
    .add("B")
    .add("C")
    .build();

// De generate (infinito)
Stream<Double> random = Stream.generate(Math::random).limit(10);
Stream<Integer> integers = Stream.iterate(0, n -> n + 2).limit(10);

// De rango
IntStream range = IntStream.range(1, 10);           // 1-9
IntStream rangeClosed = IntStream.rangeClosed(1, 10); // 1-10

// De String
IntStream chars = "hello".chars();
Stream<String> split = Pattern.compile(",").splitAsStream("a,b,c");
```

## Operaciones Intermedias (Lazy)

```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// filter - filtra elementos
Stream<Integer> filtered = numbers.stream()
    .filter(n -> n % 2 == 0);  // [2, 4, 6, 8, 10]

// map - transforma elementos
Stream<Integer> mapped = numbers.stream()
    .map(n -> n * 2);  // [2, 4, 6, ..., 20]

// flatMap - aplana y transforma
List<List<Integer>> nested = List.of(List.of(1, 2), List.of(3, 4));
Stream<Integer> flat = nested.stream()
    .flatMap(List::stream);  // [1, 2, 3, 4]

// distinct - elimina duplicados
Stream<Integer> distinct = Stream.of(1, 2, 1, 3, 2)
    .distinct();  // [1, 2, 3]

// sorted - ordena
Stream<Integer> sorted = numbers.stream()
    .sorted();  // [1, 2, 3, ..., 10]

Stream<String> sortedByLength = List.of("aa", "b", "ccc").stream()
    .sorted(Comparator.comparing(String::length));

// peek - debugging (no consume)
Stream<Integer> peeked = numbers.stream()
    .filter(n -> n > 5)
    .peek(n -> System.out.println("Filtered: " + n));

// limit - limita cantidad
Stream<Integer> limited = Stream.iterate(0, n -> n + 1).limit(10);

// skip - salta elementos
Stream<Integer> skipped = numbers.stream().skip(5);  // [6, 7, 8, 9, 10]

// takeWhile / dropWhile (Java 9+)
Stream<Integer> take = numbers.stream()
    .takeWhile(n -> n < 5);  // [1, 2, 3, 4]
```

## Operaciones Terminales (Eager)

```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);

// forEach / forEachOrdered
numbers.stream().forEach(System.out::println);
numbers.parallelStream().forEachOrdered(System.out::println);

// collect - acumula a colección
List<Integer> list = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

Set<Integer> set = numbers.stream()
    .collect(Collectors.toSet());

Map<String, Integer> map = numbers.stream()
    .collect(Collectors.toMap(
        n -> "Number: " + n,
        n -> n * 10
    ));

// toList (Java 16+)
List<Integer> toList = numbers.stream().filter(n -> n > 3).toList();

// count
long count = numbers.stream().count();
long evenCount = numbers.stream().filter(n -> n % 2 == 0).count();

// min / max
Optional<Integer> min = numbers.stream().min(Integer::compareTo);
Optional<Integer> max = numbers.stream().max(Integer::compareTo);

// findFirst / findAny
Optional<Integer> first = numbers.stream().findFirst();
Optional<Integer> any = numbers.stream().findAny();

// allMatch / anyMatch / noneMatch
boolean allEven = numbers.stream().allMatch(n -> n % 2 == 0);
boolean anyGreater5 = numbers.stream().anyMatch(n -> n > 5);
boolean noneNegative = numbers.stream().noneMatch(n -> n < 0);

// reduce - combina elementos
Optional<Integer> sum = numbers.stream().reduce(Integer::sum);
int sumWithInit = numbers.stream().reduce(0, Integer::sum);
String concat = List.of("a", "b", "c").stream()
    .reduce("", (a, b) -> a + b);  // "abc"

// toArray
Integer[] array = numbers.stream().toArray(Integer[]::new);
```

## Collectors

```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// toList / toSet
List<Integer> toList = numbers.stream().collect(Collectors.toList());
Set<Integer> toSet = numbers.stream().collect(Collectors.toSet());

// toCollection
LinkedList<Integer> linkedList = numbers.stream()
    .collect(Collectors.toCollection(LinkedList::new));

// joining
String joined = List.of("a", "b", "c").stream()
    .collect(Collectors.joining(", "));  // "a, b, c"

// counting
long count = numbers.stream().collect(Collectors.counting());

// summing/averaging
int sum = numbers.stream().collect(Collectors.summingInt(Integer::intValue));
double avg = numbers.stream().collect(Collectors.averagingInt(Integer::intValue));

// summarizing
IntSummaryStatistics stats = numbers.stream()
    .collect(Collectors.summarizingInt(Integer::intValue));
// stats.getCount(), getSum(), getMin(), getMax(), getAverage()

// groupingBy
Map<Integer, List<Integer>> grouped = numbers.stream()
    .collect(Collectors.groupingBy(n -> n % 2 == 0 ? "even" : "odd"));
// {even=[2, 4, 6, 8, 10], odd=[1, 3, 5, 7, 9]}

// partitioningBy
Map<Boolean, List<Integer>> partitioned = numbers.stream()
    .collect(Collectors.partitioningBy(n -> n > 5));
// {false=[1, 2, 3, 4, 5], true=[6, 7, 8, 9, 10]}

// mapping
Map<Integer, Set<String>> mapped = numbers.stream()
    .collect(Collectors.groupingBy(
        n -> n % 2,
        Collectors.mapping(n -> "Num:" + n, Collectors.toSet())
    ));

// flatMapping
Map<Integer, List<String>> flatMapped = numbers.stream()
    .collect(Collectors.groupingBy(
        n -> n % 2,
        Collectors.flatMapping(
            n -> Stream.of("pos:" + n, "neg:" + (-n)),
            Collectors.toList()
        )
    ));

// reducing
int product = numbers.stream()
    .collect(Collectors.reducing(1, (a, b) -> a * b));

// collectingAndThen
List<Integer> immutable = numbers.stream()
    .filter(n -> n > 3)
    .collect(Collectors.collectingAndThen(Collectors.toList(), List::copyOf));
```

## Streams Primitivos

```java
// IntStream
IntStream intStream = IntStream.rangeClosed(1, 10);
int sum = IntStream.rangeClosed(1, 100).sum();
OptionalInt max = IntStream.of(1, 2, 3, 4, 5).max();

// LongStream
LongStream longStream = LongStream.iterate(0, n -> n + 2).limit(10);

// DoubleStream
DoubleStream doubleStream = DoubleStream.generate(Math::random).limit(100);
double avg = DoubleStream.of(1.0, 2.0, 3.0).average().orElse(0);

// Mapear a primitivos
List<Integer> nums = List.of(1, 2, 3);
IntStream intStream = nums.stream().mapToInt(Integer::intValue);

// Boxing
IntStream.of(1, 2, 3).boxed().collect(Collectors.toList());

// Statistics
IntSummaryStatistics stats = IntStream.of(1, 2, 3, 4, 5).summaryStatistics();
```
