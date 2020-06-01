# Basic Authentication

![Release](https://img.shields.io/github/release/gofiber/basicauth.svg)
[![Discord](https://img.shields.io/badge/discord-join%20channel-7289DA)](https://gofiber.io/discord)
![Test](https://github.com/gofiber/basicauth/workflows/Test/badge.svg)
![Security](https://github.com/gofiber/basicauth/workflows/Security/badge.svg)
![Linter](https://github.com/gofiber/basicauth/workflows/Linter/badge.svg)

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
| Filter | `func(*fiber.Ctx) bool` | Defines a function to skip middleware | `nil` |
| Users | `map[string][string]` | Users defines the allowed credentials | `nil` |
| Realm | `string` | Realm is a string to define the realm attribute | `Restricted` |
| Authorizer | `func(string, string) bool` | A function you can pass to check the credentials however you want. | `nil` |
| Unauthorized | `func(*fiber.Ctx)` | Custom response body for unauthorized responses | `nil` |

### Example
```go
package main

import (
  "fmt"

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
    username := c.Locals("username").(string)
    password := c.Locals("password").(string)
    fmt.Println(username, password)
    c.Send("Welcome!")
  })

  app.Listen(3000)
}
```
### Test
```curl
curl --user john:doe http://localhost:3000
```
