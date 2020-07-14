# net
This package extends [golang.org/x/net](https://godoc.org/golang.org/x/net/html) with line number metadata incrusted in every node and token.

## tokenize
```
z := html.NewTokenizer(r)

for {
   z.Next()
   if tt == html.ErrorToken {
      break
   }
  
   tok := z.Token()
   fmt.Println(tok.LineNumber) // => Line where the token was defined in document.
}
```

## parse
```
doc, err := html.Parse(r)
if err != nil {
   // ...
}

var f func(*html.Node)
f = func(n *html.Node) {

   fmt.Println(n.Data, n.LineNumber) // => Line where the node was defined in document.
  
   for c := n.FirstChild; c != nil; c = c.NextSibling {
      f(c)
   }
}
f(doc)
```
