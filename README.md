## Handling Golang Modules

### Information


### History
- 2018/09/11 [Migrating from dep to Go 1.11 modules](https://blog.callr.tech/migrating-from-dep-to-go-1.11-modules/)
- 2018/08/18 [Introduction to Go Modules](https://roberto.selbach.ca/intro-to-go-modules/)
- 2018/07/21 [Everything you need to know about Packages in Go](https://medium.com/rungo/everything-you-need-to-know-about-packages-in-go-b8bac62b74cc)
- 2018/07/14 [Taking Go modules for a spin](https://dave.cheney.net/2018/07/14/taking-go-modules-for-a-spin)


### Tips
- [Go get cannot find local packages when using modules](https://stackoverflow.com/questions/52079662/go-get-cannot-find-local-packages-when-using-modules)
```
module example.com/localModule

require example.com/localModule/model v0.0.0
replace example.com/localModule/model v0.0.0 => ./model
```
