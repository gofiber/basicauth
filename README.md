```
go get -u github.com/gofiber/basicauth
```

```go
package main

import 
  "github.com/gofiber/fiber"
  "github.com/gofiber/basicauth"
)

func main() {
	app := fiber.New()

	cfg := basicauth.Config{
		Users: map[string]string{
			"john": "doe",
			"admin": "123456",
		},
	}
	app.Use(basicauth.New(cfg))

	app.Get("/", func(c *fiber.Ctx) {
		c.Send("Welcome!")
	})

	app.Listen(3000)
}
``````
go get -u github.com/gofiber/basicauth
```

```go
package main

import 
  "github.com/gofiber/fiber"
  "github.com/gofiber/basicauth"
)

func main() {
	app := fiber.New()

	cfg := basicauth.Config{
		Users: map[string]string{
			"john": "doe",
			"admin": "123456",
		},
	}
	app.Use(basicauth.New(cfg))

	app.Get("/", func(c *fiber.Ctx) {
		c.Send("Welcome!")
	})

	app.Listen(3000)
}
```
