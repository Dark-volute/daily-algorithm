[https://leetcode-cn.com/problems/xx4gT2/](https://leetcode-cn.com/problems/xx4gT2/)


## 思路
最小堆


## 代码
```go
package main
 
import (
    "container/heap"
    "fmt"
)


type IntHeap []int
 
func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] } // 最小堆  > 最大堆
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }
 
func (h *IntHeap) Push(x interface{}) {
    *h = append(*h, x.(int))
}
 
func (h *IntHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func findKthLargest(nums []int, k int) int {
	h := &IntHeap{}
    heap.Init(h)
	for i := 0; i < len(nums); i++ {
		if (i < k) {
			heap.Push(h, nums[i])
		} else if (nums[i] > (*h)[0]) {
			heap.Pop(h)
			heap.Push(h, nums[i])
		}
	}
	fmt.Println(h)
	return 	heap.Pop(h).(int)
}

func main() {
	s := []int{2,1,2,5,7,6,6}
	k := findKthLargest(s, 2)
	fmt.Println(k)
}
```
