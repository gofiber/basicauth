### Basic Authentication
Basic auth middleware provides an HTTP basic authentication. It calls the next handler for valid credentials and `401 Unauthorized` for missing or invalid credentials.

### Install
```
go get -u github.com/gofiber/fiber
go get -u github.com/gofiber/basicauth
```

### Signature
```go
basicauth.New(config ...basicauth.Config) func(*fiber.Ctx)
```

### Config
| Property | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| Skip | `func(*Ctx) bool` | Defines a function to skip middleware | `nil` |
| Users | `map[string][string]` | Users defines the allowed credentials | `nil` |
| Realm | `string` | Realm is a string to define the realm attribute | `Restricted` |

### Example
```go
package main

import (
  "github.com/gofiber/fiber"
  "github.com/gofiber/basicauth"
)

func main() {
  app := fiber.New()

  cfg := basicauth.Config{
    Users: map[string]string{
      "john":   "doe",
      "admin":  "123456",
    },
  }
  app.Use(basicauth.New(cfg))

  app.Get("/", func(c *fiber.Ctx) {
    c.Send("Welcome!")
  })

  app.Listen(3000)
}
```
### Test
```curl
curl --user john:doe http://localhost:3000
```
