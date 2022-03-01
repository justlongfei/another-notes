- #golang
- 基础使用
  ```bash
  go test -cover
  go test -coverprofile=coverage.out
  go tool cover -func=coverage.out
  go tool cover -html=coverage.out
  ```
- -covermode
	- set: did each statement run?(default)
	- count: how many times did each statement run?
	- atomic: like count, but counts precisely in parallel programs
- 参考资料
	- https://go.dev/blog/cover