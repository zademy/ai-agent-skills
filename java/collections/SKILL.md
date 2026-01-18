---
name: collections
description: Collections Framework in Java
---

# Java Collections Framework

## Interfaces Hierarchy

```
Iterable
├── Collection
│   ├── List (Ordered, duplicates)
│   ├── Set (Unique, no duplicates)
│   └── Queue (FIFO, processing order)
└── Map (Key-Value pairs)
```

## List Implementations

```java
// ArrayList - acceso rápido por índice
List<String> arrayList = new ArrayList<>();
arrayList.add("A");
arrayList.add("B");
arrayList.get(0);  // "A"
arrayList.remove(0);

// LinkedList - inserciones/borrados rápidos
LinkedList<String> linkedList = new LinkedList<>();
linkedList.addFirst("A");
linkedList.addLast("B");
linkedList.removeFirst();
linkedList.removeLast();

// Vector - sincronizado (thread-safe)
Vector<String> vector = new Vector<>();
```

## Set Implementations

```java
// HashSet - hash table, O(1)
Set<String> hashSet = new HashSet<>();
hashSet.add("A");
hashSet.add("B");
hashSet.add("A");  // Ignorado (duplicado)

// LinkedHashSet - mantiene orden de inserción
LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();

// TreeSet - árbol balanceado, O(log n), ordenado
TreeSet<String> treeSet = new TreeSet<>();
treeSet.add("B");
treeSet.add("A");  // Ordenado: A, B
treeSet.first();   // "A"
treeSet.last();    // "B"
treeSet.lower("B"); // "A"
treeSet.higher("A"); // "B"

// EnumSet - para enums
enum Color { RED, GREEN, BLUE }
EnumSet<Color> enumSet = EnumSet.allOf(Color.class);
```

## Queue Implementations

```java
// LinkedList como Queue
Queue<String> queue = new LinkedList<>();
queue.offer("A");      // Add (retorna false si full)
queue.offer("B");
String head = queue.peek();  // Mira sin remover
String removed = queue.poll();  // Remove y retorna

// PriorityQueue - heap, menor primero
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(5);
pq.offer(2);
pq.offer(8);
pq.poll();  // 2 (menor)

// ArrayDeque - double ended queue
ArrayDeque<String> deque = new ArrayDeque<>();
deque.addFirst("A");
deque.addLast("B");
deque.removeFirst();
deque.removeLast();
```

## Map Implementations

```java
// HashMap - O(1) promedio
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("A", 1);
hashMap.put("B", 2);
hashMap.get("A");  // 1
hashMap.getOrDefault("C", 0);  // 0
hashMap.containsKey("A");
hashMap.containsValue(1);

// LinkedHashMap - orden de inserción
LinkedHashMap<String, Integer> linkedMap = new LinkedHashMap<>();

// TreeMap - O(log n), ordenado por clave
TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("B", 2);
treeMap.put("A", 1);
treeMap.firstKey();  // "A"
treeMap.lastKey();   // "B"
treeMap.lowerKey("B"); // "A"

// EnumMap - para enums como claves
EnumMap<Color, String> enumMap = new EnumMap<>(Color.class);
```

## Utility Methods

```java
import java.util.Collections;
import java.util.Comparator;

// Sorting
List<Integer> list = new ArrayList<>(List.of(3, 1, 2));
Collections.sort(list);  // [1, 2, 3]
Collections.sort(list, Comparator.reverseOrder());  // [3, 2, 1]

// Binary search (requiere lista ordenada)
int index = Collections.binarySearch(list, 2);

// Reverse
Collections.reverse(list);

// Shuffle
Collections.shuffle(list);

// Unmodifiable
List<String> unmodifiable = Collections.unmodifiableList(list);

// Synchronized
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());

// Empty collections
List.empty();
Map.empty();
Set.empty();
```

## Iterators

```java
List<String> list = new ArrayList<>(List.of("A", "B", "C"));

// Iterator
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String item = iterator.next();
    if (item.equals("B")) {
        iterator.remove();  // Elimina durante iteración
    }
}

// ListIterator (bidireccional)
ListIterator<String> listIterator = list.listIterator();
while (listIterator.hasNext()) {
    int idx = listIterator.nextIndex();
    String item = listIterator.next();
    listIterator.set(item.toUpperCase());  // Modificar
}

// forEachRemaining
iterator.forEachRemaining(System.out::println);
```

## Stream Collections

```java
// Convertir a Stream
List<String> list = List.of("A", "B", "C");
list.stream();
list.parallelStream();  // Paralelo

// Collectors
List<String> result = list.stream()
    .map(String::toLowerCase)
    .filter(s -> s.startsWith("a"))
    .collect(Collectors.toList());

Map<String, Integer> map = list.stream()
    .collect(Collectors.toMap(
        s -> s,
        String::length
    ));
```
