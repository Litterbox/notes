#Curl Examples

responds with all books

```
curl http://localhost:3000/books
```

responds with book 1

```
curl http://localhost:3000/books/1
```
responds with error

```
curl http://localhost:3000/books/4
```

deletes the book

```
curl -X DELETE http://localhost:3000/books/1
```

create a book

```
curl -X POST http://localhost:3000/books?book[name]=blah&book[author]=someone
```
