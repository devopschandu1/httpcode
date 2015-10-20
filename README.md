httpcode
=======



[![Build Status](https://travis-ci.org/sckott/httpcode.svg)](https://travis-ci.org/sckott/httpcode)

`httpcode` is a tiny R package to search for and show http code messages and description. It's a port of the Python `httpcode` library. 

`httpcode` has no dependencies.

## Installation

Stable version


```r
install.packages("httpcode")
```

Development version


```r
devtools::install_github("sckott/httpcode")
```


```r
library("httpcode")
```

## Search by http code


```r
http_code(100)
#> <Status code: 100>
#>   Message: Continue
#>   Explanation: Request received, please continue
```


```r
http_code(400)
#> <Status code: 400>
#>   Message: Bad Request
#>   Explanation: Bad request syntax or unsupported method
```


```r
http_code(503)
#> <Status code: 503>
#>   Message: Service Unavailable
#>   Explanation: The server cannot process the request due to a high load
```


```r
http_code(999)
#> Error: No description found for code: 999
```

# Fuzzy code search


```r
http_code('1xx')
#> [[1]]
#> <Status code: 100>
#>   Message: Continue
#>   Explanation: Request received, please continue
#> 
#> [[2]]
#> <Status code: 101>
#>   Message: Switching Protocols
#>   Explanation: Switching to new protocol; obey Upgrade header
#> 
#> [[3]]
#> <Status code: 102>
#>   Message: Processing
#>   Explanation: WebDAV; RFC 2518
```


```r
http_code('3xx')
#> [[1]]
#> <Status code: 300>
#>   Message: Multiple Choices
#>   Explanation: Object has several resources -- see URI list
#> 
#> [[2]]
#> <Status code: 301>
#>   Message: Moved Permanently
#>   Explanation: Object moved permanently -- see URI list
#> 
...
```


```r
http_code('30[12]')
#> [[1]]
#> <Status code: 301>
#>   Message: Moved Permanently
#>   Explanation: Object moved permanently -- see URI list
#> 
#> [[2]]
#> <Status code: 302>
#>   Message: Found
#>   Explanation: Object moved temporarily -- see URI list
```


```r
http_code('30[34]')
#> [[1]]
#> <Status code: 303>
#>   Message: See Other
#>   Explanation: Object moved -- see Method and URL list
#> 
#> [[2]]
#> <Status code: 304>
#>   Message: Not Modified
#>   Explanation: Document has not changed since given time
```

## Search by message


```r
http_search("request")
#> [[1]]
#> <Status code: 100>
#>   Message: Continue
#>   Explanation: Request received, please continue
#> 
#> [[2]]
#> <Status code: 200>
#>   Message: OK
#>   Explanation: Request fulfilled, document follows
#> 
...
```


```r
http_search("forbidden")
#> [[1]]
#> <Status code: 403>
#>   Message: Forbidden
#>   Explanation: Request forbidden -- authorization will not help
```


```r
http_search("too")
#> [[1]]
#> <Status code: 413>
#>   Message: Request Entity Too Large
#>   Explanation: Entity is too large.
#> 
#> [[2]]
#> <Status code: 414>
#>   Message: Request-URI Too Long
#>   Explanation: URI is too long.
```


```r
http_search("birds")
#> Error: No status code found for search: : birds
```


## Bugs/features?

See [issues](https://github.com/sckott/httpcode/issues)
