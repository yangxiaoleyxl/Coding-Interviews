## ACM 模式的IO
以下是 ACM 模式的 IO 模板，以便笔试中快速套用（以Pyhton3为例）： 

- [ A+B(1) ]( https://ac.nowcoder.com/acm/contest/5657/A )  
```python 
import sys 
for line in sys.stdin: 
    a = line.split()  
    a = list(map(int, a)) 
    print(sum(a))  
``` 

- [ A+B(2) ]( https://ac.nowcoder.com/acm/contest/5657/B )  
```python 
import sys 
x = int(input()) 

for i in range(x):
    num = input().split() 
    print( int(num[0]) + int(num[1]) ) 
```  

- [ A+B(3) ]( https://ac.nowcoder.com/acm/contest/5657/C )  
```python 
while True: 
    s = input().split() # 一行一行读取
    a, b = int(s[0]), int(s[1])
    if not a or not b: # 遇到 0, 0 则中断
        break 
    print(a + b) 
```  

- [ A+B(4) ]( https://ac.nowcoder.com/acm/contest/5657/D )  
```python 
while True:
    s = input().split() 
    res = sum(list(map(int, s[1::]))) # 不算第一个元素
    if not res: 
        break  
    print(res) 
```   

- [ A+B(5) ]( https://ac.nowcoder.com/acm/contest/5657/E )  
```python 
num = int(input())  #  已知输入有几行
for i in range(num):
    a = input().split() 
    print(sum(list(map(int, a[1::]))))
```    

- [ A+B(6) ]( https://ac.nowcoder.com/acm/contest/5657/F )  
```python 
import sys 

for line in sys.stdin:
    s = line.split()  
    print(sum(list(map(int, s[1::]))))
```   

- [ A+B(7) ]( https://ac.nowcoder.com/acm/contest/5657/G )  
```python 
import sys 
for line in sys.stdin: 
    num = list(map(int, line.strip().split() ))  
    print(sum(num))
```  

小结：
```python 
import sys 
for line in sys.stdin:
    s = line.strip().split()  # 用于读取每行输入元素 

######################
list(map(int, x))  #  将读取的一行字符串转为int的技巧 
``` 

- [ Sort String (1) ]( https://ac.nowcoder.com/acm/contest/5657/E )  
```python 
import sys 
for line in sys.stdin: 
    a = line.split()  
    if a:
        a.sort() 
        print(' '.join(a)) 
    else:
        break
```   

- [ Sort String (2) ]( https://ac.nowcoder.com/acm/contest/5657/E )  
```python 
import sys 
for line in sys.stdin: 
    a = line.split()  
    if a:
        a.sort() 
        print(' '.join(a)) 
    else:
        break
```    

- [ Sort String (3) ]( https://ac.nowcoder.com/acm/contest/5657/J )  
```python 
import sys 

for line in sys.stdin:
    a = line.strip().split(',')  # 可去除\n
    a.sort() 
    print( ','.join(a) )
```  

- [ 平均绩点 ]( https://kamacoder.com/problem.php?id=1006 )   

```python 
while 1:
    try: 
        n = input().replace(" ", "").replace("A", "4").replace("B", "3").replace("C", "2").replace("D", "1").replace("F", "0") 
        s = 0 
        for i in n:
            if i not in "43210":
                print("Unknown") 
                break 
            s += int(i) 
        else:
            print(f"{s / len(n): .2f}")   
    except: 
        break
```   

- [ 摆平积木 ]( https://kamacoder.com/problem.php?id=1007 ) 

```python 
while 1:
    try:
        n = int( input() ) 
        ls = list( map(int, input().split() ) ) 
        ls.sort() 
        m = sum(ls) // n 
        moves = 0 
        for i in ls:
            moves += abs(i-m) 
        print(moves // 2) 
        print() 
    except: 
        break 
```  

- [ 奇怪的信 ]( https://kamacoder.com/problem.php?id=1008 ) 
```python 
while 1:
    try:
        n = int(input())
        res = 0  
        while n: 
            each = n % 10   
            if each % 2 == 0:
                res += each 
            n = n // 10 
        print(res) 
        print()
    except: 
        break
```  

- [ 运营商活动 ]( https://kamacoder.com/problem.php?id=1009 ) 
```python 
while True:
    M, K = map(int, input().split()) 
    if M == 0 or K == 0:
        break 
    res = M 
    while M >= K:
        res += M // K 
        M = M // K + M % K  # 更新奖励，新奖励 = 商 + 余数 
    print(res)  
```   

- [ 句子缩写 ]( https://kamacoder.com/problem.php?id=1013 ) 
```python 
while True: 
    # 1. 养成 try except 习惯
    # 2. 善用 list(map( ))，这种总用于 整个 list 元素的高效结构
    # 3. 字符串的常用方法： .lower(), .upper(), ''.join() 
    try: 
        n = int(input())   
        for _ in range(n):
            strs = input().split()  
            first = list(map(lambda x: (x[0]).upper(), strs) )   
            res = ''.join(first)
            print(res) 
    except:
        break
```   


- [ 神秘字符 ]( https://kamacoder.com/problem.php?id=1014 ) 
```python 
n = int(input())
for _ in range(n):
    line1 = input()
    line2 = input()
    mid = len(line1) // 2
    result = line1[:mid] + line2 + line1[mid:]
    print(result)
```

- [ 位置互换 ]( https://kamacoder.com/problem.php?id=1015 ) 
```python 
C = int(input())
for _ in range(C):
    s = input()
    even_chars = s[1::2]
    odd_chars = s[::2]
    result = ''.join(e + o for e, o in zip(even_chars, odd_chars))
    print(result)
```  

- [ 出栈的合法性 ]( https://kamacoder.com/problem.php?id=1016 ) 
```python 
while True:
    n = int(input())
    if n == 0:
        break
    sequence = list(map(int, input().split()))
    stack = []
    current = 1
    possible = True
    for num in sequence:
        while current <= num:
            stack.append(current)
            current += 1
        if stack[-1] == num:
            stack.pop()
        else:
            possible = False
            break
    if possible:
        print('Yes')
    else:
        print('No') 
```   
思路：用一个辅助栈，将**入栈序列以某种顺序入栈，看是否可以产生出栈序列**即可 
步骤：
- 若辅助栈为空，且入栈序列不为空，则入栈序列下一个元素入辅助栈
- 若 <font color="red"> 当前辅助栈的栈顶元素不等于出栈序列的首元素 </font>，那么入栈序列一直入栈，直到入栈序列为空 
- 若 当前辅助栈的栈顶元素 等于 出栈序列首元素，那么 <font color="red"> 栈顶元素弹出，出栈序列第一个元素移走 </font> 
- 若入栈序列为空，出栈序列首元素 != 栈顶元素，则出栈序列不合法

- [ 单链表反转 ]( https://kamacoder.com/problem.php?id=1018 ) 
```python  
class LinkedNode:
    def __init__(self, val=0, next=None):
        self.val = val 
        self.next = next  
        
def reverseList(head: LinkedNode) -> LinkedNode:
    temp = None # 保存cur的下一个节点
    cur = head
    pre = None
    while cur:
        temp = cur.next
        cur.next = pre # 翻转操作
        pre = cur # 更新pre 和 cur指针
        cur = temp
    return pre 
    
def printLinkedList(head): 
    cur = head 
    while cur:  
        print(cur.val, end=' ') 
        cur = cur.next 
    print()
    
while True:
    try:
        n, *nums = map(int, input().split())
    except:
        break
```   

- [ 前序和中序构造后序二叉树 ]( https://kamacoder.com/problem.php?id=1020 ) 
```python 
class Node:
    def __init__(self, val=None, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def build_tree(preorder, inorder):
    if not preorder or not inorder:
        return None
    root_val = preorder[0]
    root_index = inorder.index(root_val)
    left_inorder = inorder[:root_index]
    right_inorder = inorder[root_index+1:]
    left_preorder = preorder[1:len(left_inorder)+1]
    right_preorder = preorder[len(left_inorder)+1:]
    root = Node(root_val)
    root.left = build_tree(left_preorder, left_inorder)
    root.right = build_tree(right_preorder, right_inorder)
    return root

def postorder_traversal(root):
    if not root:
        return []
    left = postorder_traversal(root.left)
    right = postorder_traversal(root.right)
    return left + right + [root.val]

while True:
    try:
        preorder, inorder = map(str, input().split())
        if not preorder or not inorder:
            break
        root = build_tree(preorder, inorder)
        postorder = postorder_traversal(root)
        print(''.join(postorder))
    except EOFError:
        break 
``` 

- [ 二叉树的遍历 ]( https://kamacoder.com/problem.php?id=1021 ) 
```python 
class Node:
    def __init__(self, val): 
        self.val = val  
        self.left = None 
        self.right = None 
    
def preorder(root): 
    if not root: return []   
    left = preorder(root.left)
    right = preorder(root.right) 
    return [root.val] + left + right
    
def inorder(root):   
    if not root : return [] 
    left = inorder(root.left) 
    right = inorder(root.right)   
    return left + [root.val] + right

def postorder(root): 
    if not root : return [] 
    left = postorder(root.left) 
    right = postorder(root.right) 
    return left + right + [root.val] 
        
n = int(input())
nodes = [None] * (n + 1)
line_in = []
for i in range(n):
    line = input().split()
    val, left, right = line[0], int(line[1]), int(line[2])
    if not nodes[i+1]:
        node = Node(val)
        nodes[i + 1] = node
    else:
        # 更新val
        nodes[i + 1].val = val
    if left != 0:
        # 创建一个node,放入nodes列表
        node_left = Node('x')
        nodes[left] = node_left
        nodes[i + 1].left = node_left
    if right != 0:
        node_right = Node('x')
        nodes[right] = node_right
        nodes[i + 1].right = node_right

root = nodes[1]
pre = preorder(root)
ino = inorder(root)
post = postorder(root)
print(''.join(pre))
print(''.join(ino))
print(''.join(post))
```








        
        
        
        
