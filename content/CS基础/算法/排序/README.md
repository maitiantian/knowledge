# 目录

<sub>（带*标的属于八大排序）</sub>

* [比较排序](#比较排序)
    * [直接插入排序（Straight Insertion Sort）*](#直接插入排序（straight-insertion-sort）)
    * [希尔排序（Shell Sort）*](#希尔排序（shell-sort）)
    * [简单选择排序（Simple Select Sort）*](#简单选择排序（simple-select-sort）)
    * [堆排序（Heap Sort）*](#堆排序（heap-sort）)
    * [冒泡排序（Bubble Sort）*](#冒泡排序（bubble-sort）)
    * [快速排序（Quick Sort）*](#快速排序（quick-sort）)
    * [归并排序（Merge Sort）*](#归并排序（merge-sort）)
* [非比较排序](#非比较排序)
    * [基数排序（Radix Sort）*](#基数排序（radix-sort）)
    * [计数排序（Counting Sort）](#计数排序（counting-sort）)
    * [桶排序（Bucket Sort）](#桶排序（bucket-sort）)



<table>
	<tr>
		<th rowspan="2">排序方法</th>
		<th colspan="3">时间复杂度</th>
		<th>空间复杂度</th>
		<th rowspan="2">稳定性</th>
	</tr>
	<tr>
		<th>平均情况</th>
		<th>最好情况</th>
		<th>最坏情况</th>
		<th>辅助存储</th>
	</tr>
	<tr>
		<th>直接插入排序（Straight Insertion Sort）</th>
		<td>O(n<sup>2</sup>)</td>
		<td>O(n)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(1)</td>
		<td>稳定</td>
	</tr>
	<tr>
		<th>希尔排序（Shell Sort）</th>
		<td>O(n<sup>1.3</sup>)</td>
		<td>O(n)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(1)</td>
		<td>不稳定</td>
	</tr>
	<tr>
		<th>简单选择排序（Simple Select Sort）</th>
		<td>O(n<sup>2</sup>)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(1)</td>
		<td>不稳定</td>
	</tr>
	<tr>
		<th>堆排序（Heap Sort）</th>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>不稳定</td>
	</tr>
	<tr>
		<th>冒泡排序（Bubble Sort）</th>
		<td>O(n<sup>2</sup>)</td>
		<td>O(n)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(1)</td>
		<td>稳定</td>
	</tr>
	<tr>
		<th>快速排序（Quick Sort）</th>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(n<sup>2</sup>)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>不稳定</td>
	</tr>
	<tr>
		<th>归并排序（Merge Sort）</th>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(nlog<sub>2</sub>n)</td>
		<td>O(n)</td>
		<td>稳定</td>
	</tr>
	<tr>
		<th>基数排序（Radix Sort）</th>
		<td>O(d(r+n))</td>
		<td>O(d(n+rd))</td>
		<td>O(d(r+n))</td>
		<td>O(rd+n)</td>
		<td>稳定</td>
	</tr>
	<tr>
		<th>计数排序（Counting Sort）</th>
		<td>O()</td>
		<td>O()</td>
		<td>O()</td>
		<td>O()</td>
		<td>稳定</td>
	</tr>
	<tr>
		<th>桶排序（Bucket Sort）</th>
		<td>O()</td>
		<td>O()</td>
		<td>O()</td>
		<td>O()</td>
		<td>稳定</td>
	</tr>
</table>

**注：基数排序复杂度中，r代表关键字的基数，d代表长度，n代表关键字的个数。**



```python
class Sort():
    def __init__(self, target):
        self._target = target
    
    def show(self):
        print(self._target)
    
    def less(self, m, n):
        return self._target[m] <= self._target[n]
    
    def exch(self, m, n):
        foo = self._target[m]
        self._target[m] = self._target[n]
        self._target[n] = foo
        
    def isSorted(self):
        for i in range(len(self._target)-1):
            if not self.less(i, i+1):
                return False
        return True
    
    def sort(self):
        pass
    
    def main(self):
        print("Original List:")
        self.show()
        print("---------------------")
        self.sort()
        if self.isSorted():
            print('Sort Successfully!')
            self.show()
        else:
            print("Sort Unsuccessfully!")
            self.show()
```

## 快速排序（Quick Sort）
###### [<p align="right">back to top ▲</p>](#目录)

快速排序使用分治策略（Divide and Conquer）来把一个序列分为两个子序列：
1. 从序列中挑一个元素作为“基准”（pivot）；
2. 把所有比基准值小的元素放在基准前面，所有比基准值大的元素放在基准的后面（相同的数可以放到任一边），这个称为分区（partition）操作；
3. 对每个分区递归地进行步骤1~2，递归的结束条件是序列的大小是0或1，这时序列整体已经排序好了。

![快速排序](../../../images/cs_sort_quick_sort.gif)

```python

```