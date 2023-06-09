# Python 刷题常见的内置数据结构与算法 

- 常见内置数据类型：list, tuple, dict, set, frozenset 
- collections 模块：Counter (计数器)， deque (双端队列)， OrderedDict(有序字典)，defaultdict(默认值字典)
- heapq: 堆操作
- bisect: 二分查找   

### SummaryTable 

| 数据结构与算法 | 语言内置 | 内置库 |  
| -------- | :-: | :-: |  
| 线性结构 | list / tuple  | array/collections.namedtuple | 
| 链式结构 |   | collections.deque |
| 字典结构 | dict | collections.Counter/OrderedDict/defaultdict |
| 集合结构 | set/frozenset |   |
| 排序算法 | sorted |  |  
| 二分算法 |  | bisect模块 | 
| 堆算法 |  | heapq模块 | 
| 优先级队列 |  | queue.PriortyQueue/heapq | 
| 缓存算法 |  | functools.lru_cache (Least Recent Used, Python3)/cache | 

### Some tips and bugs 
- 字典顺序。 python3 和 python2 的 dict 有所不同， python 3.7 之后的 dict 会 **保持插入顺序（不是字典序）** 
- 矩阵。正确初始化一个不可变对象的二维数组：`dp = [[0] * col for _ in range(row) ]`, **不要使用** `dp = [[0] * n] * m`, 否则里面引用的同一个list, 修改一个都会变 
- 深浅拷贝。经常要在回溯中用到 ` res, path = [], [] `, path 是用来回溯的路径。找到一个结果的时候需要用 `res.append( path[:])` 而**不是** `res.append(path) ` , 因为这里 append 的 path 的引用，之后修改了 path 结果就是错的 ！( 或者用 `copy` 模块，但不如 `[:]` 简洁 ) 
-int 范围。Python 在数值范围建议用：`MAXINT = 2**63-1, MININT = -2**63`. 因为 python2 和 python3 的 `sys.maxsize` 不统一  
-优先级队列：使用内置 `queue.PriorityQueue` or `heapq` , 定义一个 item 类实现 “小于” magic function 即可
-缓存。Python3 的 functools 模块自带 cache (等价于 `lru_cache(maxsize=None)`) 和 lru_cache 装饰器，在需要递归记忆化搜索的时候会很方便 
- 除法变更：Python2 和 Python3 除法做了变更。负数除法统一写 `int(a/b)`, 整数除法统一写 `//`, 例如 二分法求中间值 `mid = (l+r) // 2` 或者 `mid = l + (r-l) // 2` 
- 自定义排序函数。Python2 可用 `nums.sort(cmp=lambda a, b: a - b)`, 但是 Python3 移除了 cmp 参数。 Python3 如果想要自定义排序函数，可用 `functools.cmp_to_key` , 即 `nums.sort(key=cmp_to_key(lambda a,b:a-b))`  

### Python list 技巧 
```python
# 排序嵌套 list
`l = [('a', 1), ('c', 2), ('b',3)]
sorted(l, key=lambda p:p[0]) # 根据第1个值排序，[('a', 1), ('b', 3), ('c', 2)]
sorted(l, key=lambda p:p[1]) # 根据第2个值排序，[('a', 1), ('c', 2), ('b', 3)]` 

# 同时获取最大值的下标和值
l = [1,2,5,4,3]
maxi, maxval = max(enumerate(l), key=lambda iv: iv[1]) # 2, 5 

# python3 排序list自定义函数(python2 直接用 cmp 参数， python3 需要用 cmp_to_key 转成 key 参数)
from functools import cmp_to_key
nums = [3,2,1,4,5]
sorted(nums, key=cmp_to_key(lambda a,b: a-b) ) # [1 ,2 ,3, 4, 5]
sorted(nums, key=cmp_to_key(lambda a,b: b-a) ) # [5, 4, 3, 2, 1] 

# 一行代码判断列表是否有序
issorted = all(l[i] <= l[i+1] for i in range(len(l) - 1))

# python3 一行代码求前缀和
from itertools import accumulate
presums = list(accumulate([1,2,3])) # [1, 3, 6]

# 一行代码求矩阵元素总和 https://stackoverflow.com/questions/10713150/how-to-sum-a-2d-array-in-python
allsum = sum(map(sum, matrix)) # 或者 allsum = sum((sum(row) for row in matrix))

``` 

### Python dict 技巧   

```python
# python 根据 key，value 排序字典
d = {'d': 4, 'a': 1, 'b': 2, 'c':3}
# dict sort by **key** and reverse
dict(sorted(d.items()))  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
dict(sorted(d.items(), reverse=True)) # {'d': 4, 'c': 3, 'b': 2, 'a': 1}

# dict sort by **value** and reverse
dict(sorted(d.items(), key = lambda kv:kv[1])) # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
dict(sorted(d.items(), key = lambda kv:kv[1], reverse=True)) # {'d': 4, 'c': 3, 'b': 2, 'a': 1}

# 获取字典对应的最大值对应的 key,value
mydict = {'A':4,'B':10,'C':0,'D':87}
maximum = max(mydict, key=mydict.get)  # Just use 'min' instead of 'max' for minimum.
maxk, maxv = maximum, mydict[maximum]
# 或者
maxk, maxv = max(mydict.items(), key=lambda k: k[1])

# 支持默认值的有序字典 (OrderedDict and defaultdict)  (注意是 key 插入顺序不是字典序)
# https://stackoverflow.com/questions/6190331/how-to-implement-an-ordered-default-dict
od = OrderedDict()  # collections.OrderedDict()
od[i] = od.get(i, 0) + 1 # 间接实现了 defaultdict(int) ，同时保持了插入字典的 key 顺序
```

### collections   
- Counter 
    - class that is used to count the frequency of elements in an iterable 
        - `most_common(n)` Returns a list of the n most common elements and their counts from the most common to the least
        - `elements()` Returns an iterator over the elements repeating each element as many times as its count 
        - `subtract()` Subtracts elements from an iterable or a mapping
        - `update()` Updates the counter with elements from an iterable or a mapping
- deque
    - Deque (Doubly Ended Queue) in Python is implemented using the module collections. This data structure is mainly used for queues. The FIFO queue mechanism is implemented by append() and popleft(). It’s operations are quite faster as compared to lists  
        - `append()` 
        - `appendleft()`
        - `pop()` 
        - `popleft()` 

```python
# Import required modules
import collections

# Initialize deque
Deque = collections.deque([10, 20, 30])

# Using append() to insert element at right end
# Inserts 0 at the end of deque
Deque.append(0)

# Printing modified deque
print("The deque after appending at right is:", Deque)

# Using appendleft() to insert element at left end
# Inserts 100 at the beginning of deque
Deque.appendleft(100)

# Printing modified deque
print("The deque after appending at left is: ", Deque)

# Using pop() to delete element from right end
# Deletes 0 from the right end of deque
Deque.pop()

# Printing modified deque
print("The deque after deleting from right is:", Deque);

# Using popleft() to delete element from left end
# Deletes 100 from the left end of deque
Deque.popleft()

# Printing modified deque
print("Queue:", Deque)
```
- defaultdict 
    - The functionality of both dictionaries and defaultdict are almost same except for the fact that defaultdict never raises a KeyError. **It provides a default value for the key that does not exists**   
```python 
# Counting occurances of elements in a list
from collections import defaultdict

my_list = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
my_dict = defaultdict(int)
for fruit in my_list:
    my_dict[fruit] += 1
print(my_dict)
# Output: defaultdict(<class 'int'>, {'apple': 3, 'banana': 2, 'orange': 1}) 

# Grouping elements in a list by a certain criterion 
from collections import defaultdict

my_list = ['apple', 'banana', 'avocado', 'orange', 'peach']
my_dict = defaultdict(list)
for fruit in my_list:
    my_dict[len(fruit)].append(fruit)
print(my_dict)
# Output: defaultdict(<class 'list'>, {5: ['apple', 'peach'], 6: ['banana'], 7: ['avocado', 'orange']}) 

# Creating a nested dicionary 
from collections import defaultdict

my_dict = defaultdict(lambda: defaultdict(int))
my_dict['Alice']['apples'] = 3
my_dict['Alice']['oranges'] = 2
my_dict['Bob']['bananas'] = 1
print(my_dict)
# Output: defaultdict(<function <lambda> at 0x7f8c5c1d7d08>, {'Alice': defaultdict(<class 'int'>, {'apples': 3, 'oranges': 2}), 'Bob': defaultdict(<class 'int'>, {'bananas': 1})})
``` 







### queue 
a way to implement a queue data structure 
- Queue(maxmize=0) (queue.Queue())
    - creates a new queue object  
        - `put()` 
        - `put_nowait()`
        - `get()`
        - `get_nowait()` 
        - `full()` 
        - `empty()`  
- LifoQueue (queue.LifoQueue())
    - The module queue provides a LIFO Queue which technically works as a Stack. It is usually used for communication between the different threads in the very same process   
        - `put()` 
        - `get()`
        - `qsize()` 
        - `full()` 
        - `empty()`  
- PriorityQueue()  
    - The queue.PriorityQueue module in Python is a built-in module that provides an implementation of a priority queue. A priority queue is a data structure that allows you to insert elements with a priority and retrieve them in order of priority.

    - In a PriorityQueue, elements are stored in a heap, which is a specialized tree-based data structure that satisfies the heap property. The heap property states that for every node i in the heap, the value of the parent node is less than or equal to the value of node i. This ensures that the smallest element is always at the root of the heap

        - `qsize()`: Returns the number of elements in the queue.
        - `empty()`: Returns True if the queue is empty, False otherwise.
        - `full()`: Returns True if the queue is full, False otherwise.
        - `put(item, priority)`: Adds an item to the queue with a specified priority.
        - `get()`: Removes and returns the item with the lowest priority from the queue 
```python 
import queue

# create a priority queue
q = queue.PriorityQueue()

# add elements to the queue with a priority
q.put((1, 'apple'))
q.put((3, 'banana'))
q.put((2, 'orange'))

# retrieve elements from the queue in order of priority
while not q.empty():
    print(q.get()[1])
```

### Difference between LIFOQueue and Deque

| No. | queue.LifoQueue | collections.deque |  
| -------- | :-: | :-: |  
| 1 | It implements sacks  | It implements a double-edged queue | 
| 2 | Present in **Queue** module | Present in **Collections** module |
| 3 | Allows various threads to communicate using queued data or messages | Simply intended to be a data structure | 
| 4 | Not commonly used, usually used for thread communication operations | Mostly used for data structure operations |


### heapq module  
Heap data structure is mainly used to represent a priority queue. In Python, it is available using the “heapq” module. The property of this data structure in Python is that each time the smallest heap element is popped (min-heap). Whenever elements are pushed or popped, heap structure is maintained. The heap[0] element also returns the smallest element each time. 

- `heapify(iterable)` : This function is used to convert the iterable into a heap data structure. i.e. in heap order  
```python
# importing "heapq" to implement heap queue
import heapq

# initializing list
li = [5, 7, 9, 1, 3]

# using heapify to convert list into heap
heapq.heapify(li)

# printing created heap
print ("The created heap is : ", (list(li)))
```

- `heappush(heap, ele)` : This function is used to insert the element mentioned in its arguments into a heap. **The order is adjusted**, so that heap structure is maintained.
- `heappop(heap)` : This function is used to remove and return the smallest element from the heap. **The order is adjusted**, so that heap structure is maintained 
```python
# importing "heapq" to implement heap queue
import heapq

# initializing list
li = [5, 7, 9, 1, 3]

# using heapify to convert list into heap
heapq.heapify(li)

# printing created heap
print("The created heap is : ", end="")
print(list(li))

# using heappush() to push elements into heap
# pushes 4
heapq.heappush(li, 4)

# printing modified heap
print("The modified heap after push is : ", end="")
print(list(li))

# using heappop() to pop smallest element
print("The popped and smallest element is : ", end="")
print(heapq.heappop(li))
```

- `heapify(iterable)` : This function is used to convert the iterable into a heap data structure. i.e. in heap order 

```python
nums = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]

# create a heap from the list
heapq.heapify(nums)  

# create a list of tuples
tuples = [(1, 'one'), (2, 'two'), (3, 'three')]

# create a heap from the list of tuples
heapq.heapify(tuples)
```  

- `heappushpop()`: Push an element onto a heap and then pop the smallest element from the heap  
- `heapreplace()`: Pop the smallest element from a heap and push a new element onto the heap 
```python 
import heapq

# create a heap
heap = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]

# use heappushpop() to push an element onto the heap and pop the smallest element
smallest = heapq.heappushpop(heap, 0)

# print the smallest element
print(smallest)

# use heapreplace() to pop the smallest element from the heap and push a new element
smallest = heapq.heapreplace(heap, 2)

# print the smallest element again
print(smallest)
``` 

- `nlargest(k, iterable, key = fun)`: This function is used to return the k largest elements from the iterable specified and satisfy the key if mentioned.
- `nsmallest(k, iterable, key = fun)`: This function is used to return the k smallest elements from the iterable specified and satisfy the key if mentioned 
```python 
# Python code to demonstrate working of
# nlargest() and nsmallest()

# importing "heapq" to implement heap queue
import heapq

# initializing list
li1 = [6, 7, 9, 4, 3, 5, 8, 10, 1]

# using heapify() to convert list into heap
heapq.heapify(li1)

# using nlargest to print 3 largest numbers
# prints 10, 9 and 8
print("The 3 largest numbers in list are : ", end="")
print(heapq.nlargest(3, li1))

# using nsmallest to print 3 smallest numbers
# prints 1, 3 and 4
print("The 3 smallest numbers in list are : ", end="")
print(heapq.nsmallest(3, li1))

```



    













