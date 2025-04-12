# Setting Up a Go Workspace

## 1. Install Go

First, download and install Go from the official website: https://golang.org/dl/

Verify your installation by opening a terminal and running:

```bash
go version
```

## 2. Understanding Go Workspace Concepts

Go has two main ways to organize code:

### GOPATH (Traditional Approach)

The traditional way uses a single workspace with a specific structure:

- `src/` - Contains source code files
- `pkg/` - Contains compiled package files
- `bin/` - Contains executable files

### Go Modules (Modern Approach, Recommended)

Go modules, introduced in Go 1.11, are the recommended way to manage dependencies and organize your code. They free you from the GOPATH restrictions.

### 3. Setting Up Go Modules

With Go modules, you can create projects anywhere on your filesystem. Here's how to get started:

1. Create a new directory for your project:

    ```bash
    mkdir my-go-project
    cd my-go-project
    ```

2. Initialize a new module:

    ```bash
    go mod init github.com/yourusername/my-go-project
    ```

    Replace `github.com/yourusername/my-go-project` with your own module path.

3. This creates a `go.mod` file that tracks your dependencies.

---

# Building First Go CLI Application

Let's create a simple CLI application that greets the user:

1. Create a file named `main.go` with the following content:

    ```go
    package main

    import (
        "fmt"
        "os"
    )

    func main() {
        // If no arguments provided, use a default name
        name := "World"
        if len(os.Args) > 1 {
            name = os.Args[1]
        }

        fmt.Printf("Hello, %s!\n", name)
    }
    ```

2. Run your application:

    ```bash
    go run main.go
    ```

    With an argument:

    ```bash
    go run main.go YourName
    ```

3. Build your application into an executable:

    ```bash
    go build
    ```

    This creates an executable file that you can run directly.

---

# Building A Simple Web Application

Let's create a basic web server:

1. Update `main.go` file with the following code:

    ```go
    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    func helloHandler(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, Web!")
    }

    func main() {
        http.HandleFunc("/", helloHandler)

        fmt.Println("Server starting at http://localhost:8080")
        if err := http.ListenAndServe(":8080", nil); err != nil {
            log.Fatal(err)
        }
    }
    ```

2. Run your web server:

    ```bash
    go run main.go
    ```

3. Open your browser and navigate to http://localhost:8080
