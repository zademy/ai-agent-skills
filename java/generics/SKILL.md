---
name: generics
description: >
  Generics in Java.
  Trigger: When working with Java generics - type parameters, wildcards, bounded types
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Generics"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Java Generics

## Classes Genéricas

```java
public class Box<T> {
    private T content;
    
    public void set(T content) {
        this.content = content;
    }
    
    public T get() {
        return content;
    }
}

// Uso
Box<String> stringBox = new Box<>();
stringBox.set("Hello");
String value = stringBox.get();

Box<Integer> intBox = new Box<>();
```

## Múltiples Genéricos

```java
public class Pair<K, V> {
    private K key;
    private V value;
    
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    public K getKey() { return key; }
    public V getValue() { return value; }
}
```

## Wildcards

```java
// ? extends -上限 (solo lectura)
public void process(List<? extends Number> numbers) {
    for (Number n : numbers) {
        System.out.println(n);
    }
}

// ? super -下限 (escritura)
public void addNumbers(List<? super Integer> list) {
    list.add(42);
}

// Unbounded ?
public void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

## Bounded Generic

```java
public class ComparableBox<T extends Comparable<T>> {
    private T item;
    
    public boolean isGreaterThan(T other) {
        return item.compareTo(other) > 0;
    }
}
```
