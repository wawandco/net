# net
This package extends [golang.org/x/net](https://godoc.org/golang.org/x/net/html) with line number metadata attached to every node and token inside `html' package.

## Tokenize
```
z := html.NewTokenizer(r)

for {
   z.Next()
   if tt == html.ErrorToken {
      break
   }
  
   tok := z.Token()
   fmt.Println(tok.Line) // => Line where the token was defined in document.
}
```

## Parse
```
doc, err := html.Parse(r)
if err != nil {
   // ...
}

var f func(*html.Node)
f = func(n *html.Node) {

   fmt.Println(n.Data, n.Line) // => Line where the node was defined in document.
  
   for c := n.FirstChild; c != nil; c = c.NextSibling {
      f(c)
   }
}
f(doc)
```

## quote for attributes
```
z := html.NewTokenizer(r)

for {
   ...
   tok := z.Token()
   for _, attr := range token.Attr {
		fmt.Println("quote", attr.Quote) // => ' or "
	}
}
```
## Use
Add this line to your go.mod definition file.    
`replace golang.org/x/net => github.com/larrymjordan/net v0.0.0-20200714194128-a771946c73f6` 
