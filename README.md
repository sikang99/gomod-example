## Handling Golang Modules

### Information


### History
- 2019/03/19 [Using Go Modules](https://blog.golang.org/using-go-modules)
- 2019/00/00
- 2018/12/19 [Go Modules in 2019](https://blog.golang.org/modules2019)
- 2018/10/07 [Introduction to Go Modules in Go v1.11, Goodbye GOPATH!](https://www.melvinvivas.com/go-version-1-11-modules/)
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
- gomod script function
```sh
function gomod ()
{
    if [ $# = 0 ]; then
        echo "usage: $FUNCNAME [auto|on|off|<command>...]";
        return;
    fi;
    case $1 in
        . | check)
            echo "$FUNCNAME> `go version` [`env | grep GO111MODULE`]"
        ;;
        on | off | auto)
            export GO111MODULE=$1;
            gomod check
        ;;
        init | tidy | vendor | verify | graph | why | edit | download)
            go mod $@
        ;;
        tag)
            git describe --always
        ;;
        mod)
            vi go.mod
        ;;
        sum)
            vi go.sum
        ;;
        list)
            go list -m all
        ;;
        vbuild)
            go build --mod=vendor ./...
        ;;
        rebuild)
            rm -rf go.mod go.sum vendor/;
            go mod init;
            go mod tidy;
            go mod vendor;
            go build ./...
        ;;
        clean)
            rm -f Gopkg.toml Gopkg.lock glide.yaml glide.lock vendor/vendor.json
        ;;
        *)
            go $@
        ;;
    esac
}
```
