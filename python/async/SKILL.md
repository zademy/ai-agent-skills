---
name: async
description: >
  Asynchronous programming in Python.
  Trigger: When working with async Python - async/await, asyncio, tasks, coroutines, event loop
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Python Async / Asyncio"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Python Async

## Basic async/await

```python
import asyncio

async def greet(name: str) -> str:
    await asyncio.sleep(1)  # Non-blocking sleep
    return f"Hello, {name}!"

# Run async function
result = asyncio.run(greet("John"))
print(result)  # "Hello, John!"
```

## Multiple Tasks

```python
async def fetch_data(id: int) -> dict:
    await asyncio.sleep(1)
    return {"id": id, "data": f"Data {id}"}

async def main():
    # Run concurrently
    tasks = [fetch_data(i) for i in range(1, 4)]
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())
```

## Task Management

```python
async def long_task(n: int) -> int:
    await asyncio.sleep(2)
    return n * 2

async def main():
    # Create task
    task = asyncio.create_task(long_task(10))
    
    # Do other work while task runs
    print("Task started, doing other work...")
    
    # Wait for result
    result = await task
    print(f"Result: {result}")

asyncio.run(main())
```

## Timeout and Exceptions

```python
async def slow_operation():
    await asyncio.sleep(10)
    return "Done"

async def main():
    try:
        # Timeout after 3 seconds
        result = await asyncio.wait_for(slow_operation(), timeout=3)
        print(result)
    except asyncio.TimeoutError:
        print("Operation timed out!")

asyncio.run(main())
```

## Semaphore (Rate Limiting)

```python
import asyncio

async def fetch(url: str, semaphore: asyncio.Semaphore):
    async with semaphore:
        await asyncio.sleep(1)
        return f"Fetched: {url}"

async def main():
    semaphore = asyncio.Semaphore(3)  # Max 3 concurrent
    
    urls = [f"url{i}" for i in range(10)]
    tasks = [fetch(url, semaphore) for url in urls]
    
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())
```

## Queue for Producer/Consumer

```python
import asyncio
from asyncio import Queue

async def producer(queue: Queue):
    for i in range(5):
        await asyncio.sleep(0.5)
        await queue.put(i)
        print(f"Produced: {i}")

async def consumer(queue: Queue):
    while True:
        item = await queue.get()
        await asyncio.sleep(1)
        print(f"Consumed: {item}")
        queue.task_done()

async def main():
    queue = Queue()
    
    # Start producer and consumer
    await asyncio.gather(
        producer(queue),
        consumer(queue)
    )

asyncio.run(main())
```

## Async Context Manager

```python
class Timer:
    def __enter__(self):
        self.start = asyncio.get_event_loop().time()
        return self
    
    def __exit__(self, *args):
        self.end = asyncio.get_event_loop().time()
        print(f"Elapsed: {self.end - self.start:.2f}s")

# For async context manager
class AsyncTimer:
    async def __aenter__(self):
        self.start = asyncio.get_event_loop().time()
        return self
    
    async def __aexit__(self, *args):
        self.end = asyncio.get_event_loop().time()
        print(f"Elapsed: {self.end - self.start:.2f}s")

async def main():
    async with AsyncTimer():
        await asyncio.sleep(1)

asyncio.run(main())
```
