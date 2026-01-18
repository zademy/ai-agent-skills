---
name: concurrency
description: Concurrency in Go (Goroutines and Channels)
---

# Go Concurrency

## Goroutines

```go
// Función asíncrona (goroutine)
func processTask(id int) {
    fmt.Printf("Task %d started\n", id)
    time.Sleep(time.Second)
    fmt.Printf("Task %d completed\n", id)
}

func main() {
    // Iniciar goroutine
    go processTask(1)
    go processTask(2)
    go processTask(3)
    
    // Espera a que terminen
    time.Sleep(2 * time.Second)
}
```

## Channels

```go
// Canal básico
ch := make(chan int)

// Enviar datos
ch <- 42

// Recibir datos
value := <-ch

// Canal con dirección
func sendData(ch chan<- int) {
    ch <- 10
}

func receiveData(ch <-chan int) int {
    return <-ch
}
```

## Buffered Channels

```go
// Canal con buffer
ch := make(chan int, 2)

// Puede enviar 2 sin receptor
ch <- 1
ch <- 2
// Si envío un tercero, se bloquea

// Cerrar canal
close(ch)

// Verificar si está cerrado
value, ok := <-ch
if !ok {
    fmt.Println("Channel closed")
}
```

## Select

```go
ch1 := make(chan int)
ch2 := make(chan int)

go func() { ch1 <- 1 }()
go func() { ch2 <- 2 }()

select {
case v1 := <-ch1:
    fmt.Println("Received from ch1:", v1)
case v2 := <-ch2:
    fmt.Println("Received from ch2:", v2)
case <-time.After(time.Second):
    fmt.Println("Timeout!")
}
```

## WaitGroup

```go
import "sync"

func worker(id int, wg *sync.WaitGroup) {
    defer wg.Done()  // Llama cuando termina
    fmt.Printf("Worker %d started\n", id)
    time.Sleep(time.Second)
    fmt.Printf("Worker %d completed\n", id)
}

func main() {
    var wg sync.WaitGroup
    
    for i := 1; i <= 3; i++ {
        wg.Add(1)
        go worker(i, &wg)
    }
    
    wg.Wait()  // Espera a que todos terminen
    fmt.Println("All workers completed")
}
```

## Mutex

```go
import "sync"

type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *Counter) Get() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}
```

## Context

```go
import "context"

func longOperation(ctx context.Context) error {
    for {
        select {
        case <-ctx.Done():
            return ctx.Err()
        default:
            // 작업 수행
            time.Sleep(100 * time.Millisecond)
        }
    }
}

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
    defer cancel()
    
    if err := longOperation(ctx); err != nil {
        fmt.Println("Operation cancelled:", err)
    }
}
```

## Fan-in/Fan-out

```go
func fanOut() {
    tasks := make(chan int, 10)
    
    // Workers
    var wg sync.WaitGroup
    for i := 0; i < 3; i++ {
        wg.Add(1)
        go func(workerID int) {
            defer wg.Done()
            for task := range tasks {
                fmt.Printf("Worker %d processing task %d\n", workerID, task)
            }
        }(i)
    }
    
    // Send tasks
    for i := 1; i <= 9; i++ {
        tasks <- i
    }
    close(tasks)
    
    wg.Wait()
}
```
