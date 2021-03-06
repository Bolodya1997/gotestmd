# Producer

This example shows how can be used section `Requires` for `.md` based tests.

Section `Requres` means that the included this example suite should have _required dependencies_ Otherwise, this example will be converted to a suite with a needed dependencies.

**Note:** This example has not `includes` and `requires` sections. That means this example is just provided setup and tear down logic. 
## Run

```bash
echo "Do setup logic for the suite here"
```


## Cleanup
```bash
echo "Do teardown logic for the suite here"
```

# Results

The result of generating a suite is:
```go
package producer

import (
	"os"
	"path/filepath"

	"github.com/networkservicemesh/gotestmd/pkg/suites/shell"
)

type Suite struct {
	shell.Suite
}

func (s *Suite) SetupSuite() {
	dir := filepath.Join(os.Getenv("GOPATH"), "src", "/github.com/networkservicemesh/gotestmd/examples/Producer")
	r := s.Runner(dir)
	s.T().Cleanup(func() {
		r.Run(`echo "Do teardown logic for the suite here"`)
	})
	r.Run(`echo "Do setup logic for the suite here"`)
}
func (s *Suite) Test() {}
```