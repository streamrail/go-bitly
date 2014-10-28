# go-bitly

a simple bit.ly client for go to easily shorten url's.

## usage

get the package:

```bash
    $ go get github.com/streamrail/go-bitly
```

import it, *set your auth token*, and let the party begin:
```go
package main

import (
	"flag"
	"github.com/streamrail/go-bitly"
)

var (
	token = flag.String("apiKey", "", "your bit.ly api key")
)

func TestBitly(t *testing.T) {
	flag.Parse()

	if *token == "" {
		t.Error("required flag: token")
	}

	bitlyClient := NewClient(*token)

	var testUrl = "https://www.google.com/"

	if shortUrl, err := bitlyClient.Shorten(testUrl); err != nil {
		t.Error(err.Error())
	} else {
		// do awesome stuff with shortUtl
	}
}

```

## run tests

In order to run the tests, you must *set your auth token*. The tests work by requesting bit.ly to shorten "https://www.google.com/". Then we try to http GET the shortURl, and we follow the redirect chain for 10 seconds. During those 10 seconds, if we got the original URL, we send it on a channel and the test passes.

## License

MIT (see [LICENSE](https://github.com/streamrail/go-bitly/blob/master/LICENSE) file)
