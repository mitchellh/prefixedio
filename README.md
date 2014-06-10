# prefixed-reader

`prefixed-reader` (Golang package: `prefixedreader`) is a package for Go
that takes an `io.Reader` and de-multiplexes line-oriented output based
on a line prefix to a set of readers.

## Installation and Usage

Install using `go get github.com/mitchellh/prefixed-reader`.

Below is an example of its usage ignoring errors:

```go
// Assume r is some set io.Reader. Perhaps a file, network, anything.
var r io.Reader

// Initialize the prefixed reader
pr, _ := prefixedreader.New(r)

// Grab readers for a couple prefixes
errR, _ := pr.Prefix("err: ")
outR, _ := pr.Prefix("out: ")

// Copy the data to different places based on the prefix
go io.Copy(os.Stderr, errR)
go io.Copy(os.Stdout, outR)
```
