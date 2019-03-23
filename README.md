# Making Golang Product

- [Testing](#testing)
- [Package management](#package-management)

---
## Testing
### History
- 2019/03/20 [Debugging and Testing in Golang](https://medium.com/@ibrahimpasha.m.d/debugging-and-testing-in-golang-93f4031b00d9)


---
## Package management

### Information
- [Go Modules](https://github.com/golang/go/wiki/Modules)
- [Semantic Versioning](https://semver.org/) - 2.0.0


### 국내상황
- 2018/12/10 [Go Modules 살펴보기](https://velog.io/@kimmachinegun/Go-Go-Modules-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-7cjn4soifk)


### History
- 2019/03/19 [Using Go Modules](https://blog.golang.org/using-go-modules)
- 2019/03/09 [Exposing Go Modules to Prometheus](https://povilasv.me/exposing-go-modules-to-prometheus/)
- 2019/00/00
- 2018/12/19 [Go Modules in 2019](https://blog.golang.org/modules2019)
- 2018/10/07 [Introduction to Go Modules in Go v1.11, Goodbye GOPATH!](https://www.melvinvivas.com/go-version-1-11-modules/)
- 2018/09/11 [Migrating from dep to Go 1.11 modules](https://blog.callr.tech/migrating-from-dep-to-go-1.11-modules/)
- 2018/09/01 [A gentle introduction to Golang Modules](https://ukiahsmith.com/blog/a-gentle-introduction-to-golang-modules/)
- 2018/08/26 [Using Go modules with vendor support on Travis CI](https://arslan.io/2018/08/26/using-go-modules-with-vendor-support-on-travis-ci/)
- 2018/08/18 [Introduction to Go Modules](https://roberto.selbach.ca/intro-to-go-modules/)
- 2018/07/21 [Everything you need to know about Packages in Go](https://medium.com/rungo/everything-you-need-to-know-about-packages-in-go-b8bac62b74cc)
- 2018/07/14 [Taking Go modules for a spin](https://dave.cheney.net/2018/07/14/taking-go-modules-for-a-spin)


### Tips
- [Multiple modules within the same project](https://stackoverflow.com/questions/55041915/multiple-modules-within-the-same-project)
> A module is a collection of related Go packages that are versioned together as a single unit.
> Modules record precise dependency requirements and create reproducible builds.
> Most often, a version control repository contains exactly one module defined in the repository root. 
> (Multiple modules are supported in a single repository, 
> but typically that would result in more work on an on-going basis than a single module per repository).
>
> Summarizing the relationship between repositories, modules, and packages:
> 1. A repository contains one or more Go modules.
> 2. Each module contains one or more Go packages.
> 3. Each package consists of one or more Go source files in a single directory.

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
