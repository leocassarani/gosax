# gosax

`gosax` is a Go library for XML SAX (Simple API for XML) parsing, supporting read-only functionality. This library is
designed for efficient and memory-conscious XML parsing, drawing inspiration from various sources to provide a
performant parser.

## Features

- **Read-only SAX parsing**: Stream and process XML documents without loading the entire document into memory.
- **Efficient parsing**: Utilizes techniques inspired by `quick-xml` and `pkg/json` for high performance.
- **SWAR (SIMD Within A Register)**: Optimizations for fast text processing, inspired by `memchr`.

## Installation

To install `gosax`, use `go get`:

```bash
go get github.com/orisano/gosax
```

## Usage

Here is a basic example of how to use `gosax` to parse an XML document:

```go
package main

import (
	"fmt"
	"log"
	"strings"

	"github.com/orisano/gosax"
)

func main() {
	xmlData := `<root><element>Value</element></root>`
	reader := strings.NewReader(xmlData)

	r := gosax.NewReader(reader)
	for {
		e, err := r.Event()
		if err != nil {
			log.Fatal(err)
		}
		if e.Type() == gosax.EventEOF {
			break
		}
		fmt.Println(string(e.Bytes))
	}
	// Output:
	// <root>
	// <element>
	// Value
	// </element>
	// </root>
}

```

## License

This library is licensed under the terms specified in the LICENSE file.

## Acknowledgements

`gosax` is inspired by the following projects and resources:

- [Dave Cheney's GopherCon SG 2023 Talk](https://dave.cheney.net/paste/gophercon-sg-2023.html)
- [quick-xml](https://github.com/tafia/quick-xml)
- [memchr](https://github.com/BurntSushi/memchr) (SWAR part)

## Contributing

Contributions are welcome! Please fork the repository and submit pull requests.

## Contact

For any questions or feedback, feel free to open an issue on the GitHub repository.