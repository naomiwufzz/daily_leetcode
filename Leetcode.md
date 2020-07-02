# Leetcode215 数组中第k个最大元素

解法1：调库函数排序后索引

~~~python
class Solution:
    def findKthLargest(self, nums, k):
        order_list = sorted(nums)
        result = order_list[len(nums)-k]
        return result

sol = Solution()
result1 = sol.findKthLargest([3,2,1,5,6,4], k=2)
result2 = sol.findKthLargest([3,2,3,1,2,4,5,5,6], k=4)
print('result1', result1)
print('result2', result2)
~~~

优势：python的sort解和了合并排序(merge sort)和插入排序(insertion sort)，而得出的timesort排序算法。时间很快，耗内存，空间换时间。

# 剑指 Offer 09. 用两个栈实现队列

栈是什么？

栈就(Stack)跟箱子里放书本一样。LIFO（Last in first out）。

队列(Queue)是FIFO（First in First out）

就是用两个栈，实现队列。

python没有栈这个数据格式，需要模拟。

~~~python
class CQueue:
    def __init__(self):
        self.A, self.B = [], []

    def appendTail(self, value: int) -> None:
        self.A.append(value)
        return self.A, self.B
        # print('现在的A是', self.A)
    def deleteHead(self) -> int:
        if self.B != []: #意思是，如果B里面本来就有元素，那应该，先把最最元老的元素pop掉
            return self.B.pop(),self.A, self.B
        if self.A == []:#当B是空，A也是空，没的玩了，返回-1
            return -1
        while self.A != []:#当B空掉了，当A不为空的情况才需要把A里面的元素倒入B
            self.B.append(self.A.pop())

        return self.B.pop(), self.A, self.B



print('测试')
li2 = CQueue()
print(li2.appendTail(2))
print(li2.appendTail(3))
print(li2.appendTail(4))
print(li2.appendTail(5))
print(li2.deleteHead())
print(li2.appendTail(6))
print(li2.appendTail(7))
print(li2.appendTail(8))
print(li2.deleteHead())
print(li2.deleteHead())

~~~







以下两个结果：

~~~python
[2]
[2, 3]
[2, 3, 4]
[2, 3, 4, 5]
(2, [], [5, 4, 3])
[6]
[6, 7]
[6, 7, 8]
(3, [6, 7, 8], [5, 4])
(4, [6, 7, 8], [5])

Process finished with exit code 0

([2], [])
([2, 3], [])
([2, 3, 4], [])
([2, 3, 4, 5], [])
(2, [], [5, 4, 3])
([6], [5, 4, 3])
([6, 7], [5, 4, 3])
([6, 7, 8], [5, 4, 3])
(6, [], [5, 4, 3, 8, 7])
(7, [], [5, 4, 3, 8])

Process finished with exit code 0

~~~



第二个是错的，是因为A不能在B非空的情况下，倒进去，会导致，B的顺序弄错

# 1480. 一维数组的动态和

~~~python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        
        result_list = []
        sum = 0
        for value in nums:
            sum += value
            result_list.append(sum)
        return result_list
~~~

