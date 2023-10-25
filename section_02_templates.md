## 6. Understanding templates

* [text/template](https://pkg.go.dev/text/template)
* [html/template](https://pkg.go.dev/html/template)

* Templates allow us to `Personalize Web Pages` for the users.

* Template is like a Form letter
```
Dear {first-name},

Merry Christmas!

We hope that this letter finds you well.

...
```

***

## 7. Templating with concatenation

```
name := "hello"
```

```html
`<!DOCTYPE html>
 <html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Hello World!</title>
	</head>
	<body>
	    <h1>` + name + `</h1>
	</body>
</html>`
```

```go
nf, err := os.Create("index.html")
if err != nil {
    log.Fatal("error creating file", err)
}
defer nf.Close()

// func Copy(dst Writer, src Reader) (written int64, err error)
io.Copy(nf, strings.NewReader(str))
```
***

## 8. Understanding package text/template: parsing & executing

***

## 9. Passing data into templates

***

## 10. Variables in templates

***

## 11. Passing composite data structures into templates

***

## 12. Functions in templates

***

## 13. Pipelines in templates

***

## 14. Predefined global function in templates

***

## 15. Nesting templates - modularizing your code

***

## 16. Passing data in templates & composition

***

## 17. Using methods in templates

***

## 18. Hands-on exercises

***

## 19. Using package html/template, character escaping, & cross-site
