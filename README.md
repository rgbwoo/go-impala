go-impala is a Go driver for Cloudera Impala

It's based on [impalathing](https://github.com/koblas/impalathing)

## Using
```go
package main

import (
    "log"
    "fmt"
    "time"
    impalathing "github.com/bippio/go-impala"
)

func main() {
    host := "<impala-host>"
    port := 21000

    opts := impalathing.DefaultOptions

    // enable LDAP authentication:
    opts.UseLDAP = true
    opts.Username = "<username>"
    opts.Password = "<password>"

    con, err := impalathing.Connect(host, port, &opts)
    if err != nil {
        log.Fatal(err)
    }

    query, err := con.Query(context.Background(), "<sql-query>")

    startTime := time.Now()
    results := query.FetchAll(context.Background())
    log.Printf("Fetch %d rows(s) in %.2fs", len(results), time.Duration(time.Since(startTime)).Seconds())
}

```