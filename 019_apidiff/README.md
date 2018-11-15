<!-- __JSON: gobin -m -run myitcv.io/cmd/egrunner script.sh # LONG ONLINE

## Using `apidiff` to determine API compatibility

_Preamble goes here..._

This guide makes use of the command [`apidiff`]({{PrintOut "apidiff repo"}}), a light wrapper around the
work-in-progress [`apidiff` package](https://go-review.googlesource.com/c/exp/+/143897), to analyse the changes between
two versions of the [`{{PrintOut "specialapi package"}}`]({{PrintOut "specialapi repo"}}) package.

### Walk-through

Setup ready to analyse the differences between the two versions of `{{PrintOut "specialapi package"}}`:

```
{{PrintBlock "setup" -}}
```

`v1.0.0` look like:

```go
{{PrintBlockOut "v1.0.0" -}}
```

`v2.0.0` look like:

```go
{{PrintBlockOut "v2.0.0" -}}
```

Use `apidiff` to summarise the changes:

```
{{PrintBlock "changes" -}}
```

### Version details

```
{{PrintBlockOut "version details" -}}
```

-->

## Using `apidiff` to determine API compatibility

_Preamble goes here..._

This guide makes use of the command [`apidiff`](https://github.com/go-modules-by-example-staging/apidiff), a light wrapper around the
work-in-progress [`apidiff` package](https://go-review.googlesource.com/c/exp/+/143897), to analyse the changes between
two versions of the [`github.com/go-modules-by-example-staging/specialapi`](https://github.com/go-modules-by-example-staging/specialapi) package.

### Walk-through

Setup ready to analyse the differences between the two versions of `github.com/go-modules-by-example-staging/specialapi`:

```
$ cd /home/gopher/scratchpad
$ git clone -q --branch v1.0.0 https://github.com/go-modules-by-example-staging/specialapi specialapi_v1.0.0
$ git clone -q --branch v2.0.0 https://github.com/go-modules-by-example-staging/specialapi specialapi_v2.0.0
```

`v1.0.0` look like:

```go
$ cat specialapi_v1.0.0/specialapi.go
package specialapi

const Number = 42

const RandomNumber = 4

func Name() string {
	return "Rob Pike"
}
```

`v2.0.0` look like:

```go
$ cat specialapi_v2.0.0/specialapi.go
package specialapi

const Number = "42"

const RandomNumber = 6

func FullName() string {
	return "Rob Pike"
}
```

Use `apidiff` to summarise the changes:

```
$ apidiff specialapi_v1.0.0 specialapi_v2.0.0
Incompatible changes:
- Name: removed
- Number: changed from untyped int to untyped string
- RandomNumber: value changed from 4 to 6

Compatible changes:
- FullName: added
```

### Version details

```
go version go1.11.2 linux/amd64
apidiff https://go.googlesource.com/exp refs/changes/97/143897/6
```

<!-- END -->
