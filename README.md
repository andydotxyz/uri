# uri
[![Build Status](https://travis-ci.org/fredbi/uri.svg?branch=master)](https://travis-ci.org/fredbi/uri)
[![codecov](https://codecov.io/gh/fredbi/uri/branch/master/graph/badge.svg)](https://codecov.io/gh/fredbi/uri)
[![license](http://img.shields.io/badge/license/License-MIT-yellow.svg)](https://raw.githubusercontent.com/fredbi/uri/master/LICENSE.md)
[![Go Reference](https://pkg.go.dev/badge/github.com/fredbi/uri.svg)](https://pkg.go.dev/github.com/fredbi/uri)
[![GolangCI](https://golangci.com/badges/github.com/fredbi/uri.svg)](https://golangci.com)
[![Go Report Card](https://goreportcard.com/badge/github.com/fredbi/uri)](https://goreportcard.com/report/github.com/fredbi/uri)

Package uri is meant to be an RFC 3986 compliant URI builder, parser and validator for Go.

It supports strict RFC validation for URI and URI relative references.

## Usage

##### Parsing

```go
	u, err := Parse("https://example.com:8080/path")
	if err != nil {
		fmt.Printf("Invalid URI")
	} else {
		fmt.Printf("%s", u.Scheme())
	}
	// Output: https
```

```go
	u, err := ParseReference("//example.com/path")
	if err != nil {
		fmt.Printf("Invalid URI reference")
	} else {
		fmt.Printf("%s", u.Authority().Path())
	}
	// Output: /path
```

##### Validation

```go
    isValid := IsURI("urn://example.com?query=x#fragment/path") // true
    isValid= IsURI("//example.com?query=x#fragment/path") // false

    isValid= IsURIReference("//example.com?query=x#fragment/path") // true
```

##### Building

## Reference specifications
- https://tools.ietf.org/html/rfc3986

Internationalization support:
- https://tools.ietf.org/html/rfc3987

IPv6 addressing scheme reference and erratum:
- https://tools.ietf.org/html/rfc6874

This allows for stricter conformance than the `net/url` in the Go standard libary,
which provides a workable but loose implementation of the RFC.

This package concentrates on RFC 3986 strictness for URI validation. 
At the moment, there is no attempt to normalize or auto-escape strings. 
For url normalization, see [PuerkitoBio/purell](https://github.com/PuerkitoBio/purell).

## Disclaimer

Not supported:
- provisions for "IPvFuture" are not implemented.

Hostnames vs domain names:
- a list of common schemes triggers the validation of hostname against domain name rules.

Example:

## Credits

Tests have been aggregated from test suites of URI validators from other languages:
Perl, Python, Scala, .Net. and the Go url standard library.

> This package was initially based on the work from ttacon/uri (credits: Trey Tacon).
> Extra features like MySQL URIs present in the original repo have been removed.
