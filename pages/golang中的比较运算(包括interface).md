- #golang
- [comparison operator in golang](https://go.dev/ref/spec#Comparison_operators)
	- 比较和排序是不同的，比如`Integer `是可排序的，而`Boolean `可比较不可排序
	- Slice, map, and function类型的值是不可比较的
	- [[golang]]中两个interface类型的 _值_ 是可以比较的
		- interface与interface相等：
			- 两个interface都为空，或者
			- 两个interface拥有完全相同的 _动态类型_ ，并且拥有相等的 _动态值_
		- 非interface类型的值和interface类型的值在如下情况下是可以比较的
			- 非interface类型的值是可以比较的，并且该值是interface的实现
			- 两者相等：
				- interface类型的值的 _动态类型_ 和 非interface类型的值的类型是相同的，并且
				- interface类型的值的 _动态值_ 与非interface类型的值相等
		- **如果两个interface的 _动态类型_ 相同，但是 _动态值_ 是不可以比较的，那么会造成运行时panic**
			- TODO 尝试写了一个，但是编译时就会报错，后面构造出来运行时panic的再补充。
			  :LOGBOOK:
			  CLOCK: [2022-01-26 Wed 23:46:21]--[2022-01-26 Wed 23:46:35] =>  00:00:14
			  :END:
			- ```golang
			  package main
			  
			  import "fmt"
			  
			  type base interface {
			  	Flag() string
			  }
			  
			  type b struct {
			  	test []int
			  }
			  
			  func (n *b) Flag() string {
			  	return "b"
			  }
			  
			  func main() {
			  	var g1, g2 b
			  	if g1 == g2 {
			  		fmt.Println("g1 equals g2")
			  	} else {
			  		fmt.Println("g1 not equal g2")
			  	}
			  }
			  ```
-