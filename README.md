## Handling Golang Modules

### Information


### History
- 2018/07/21 [Everything you need to know about Packages in Go](https://medium.com/rungo/everything-you-need-to-know-about-packages-in-go-b8bac62b74cc)


### Tips
- [Go get cannot find local packages when using modules](https://stackoverflow.com/questions/52079662/go-get-cannot-find-local-packages-when-using-modules)
```
module example.com/localModule

require example.com/localModule/model v0.0.0
replace example.com/localModule/model v0.0.0 => ./model
```
