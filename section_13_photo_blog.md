## 96. Starting Files

***

## 97. User Data

***

## 98. Storing Multiple Values

***

## 99. Uploading Pictures

```html
<!doctype html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>INDEX</title>
</head>

<body>

<h1>Cookie Values:</h1>
{{range .}}
<h2>{{.}}</h2>
{{end}}

<form method="post" enctype="multipart/form-data">                  # For uploading files
    <input type="file" name="nf">                                   # name = "nf"; identifier we use in `Go` code
    <input type="submit">
</form>

</body>
</html>
```

```go
func index(w http.ResponseWriter, req *http.Request) {
	c := getCookie(w, req)

	// process form submission
	if req.Method == http.MethodPost {
		mf, fh, err := req.FormFile("nf")
		if err != nil {
			fmt.Println(err)
		}
		defer mf.Close()

		// create sha for file name
		ext := strings.Split(fh.Filename, ".")[1]
		h := sha1.New()
		io.Copy(h, mf)
		fname := fmt.Sprintf("%x", h.Sum(nil)) + "." + ext

		// create new file
		wd, err := os.Getwd()
		if err != nil {
			fmt.Println(err)
		}
		path := filepath.Join(wd, "public", "pics", fname)
		nf, err := os.Create(path)
		if err != nil {
			fmt.Println(err)
		}
		defer nf.Close()

		// copy
		mf.Seek(0, 0)
		io.Copy(nf, mf)

		// add filename to this user's cookie
		c = appendValue(w, c, fname)
	}
	xs := strings.Split(c.Value, "|")
	tpl.ExecuteTemplate(w, "index.gohtml", xs)
}
```

***

## 100. Displaying Pictures

***
