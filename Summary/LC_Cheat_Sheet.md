## LC cheating sheet  

### 数组 
- 

### 链表  
- 反转链表 
```python 
class Solution:
    def ReverseList(self , head: ListNode) -> ListNode:
        # write code here 
        if not head or not head.next:
            return head  
        cur = head  
        pre = None
        while cur:
            nxt = cur.next   
            cur.next = pre 
            pre = cur 
            cur = nxt   
        return pre
``` 

- 指定区间反转
```python 
class Solution:
    def reverseBetween(self , head: ListNode, m: int, n: int) -> ListNode:
        # write code here 
        dummy = ListNode(0) 
        dummy.next = head 
        p0 = dummy
        for _ in range(m - 1):
            p0 = p0.next 
        
        pre=None
        cur = p0.next 
        for _ in range(n-m+1): 
            nxt = cur.next 
            cur.next = pre 
            pre = cur 
            cur = nxt 

        p0.next.next = cur 
        p0.next = pre  
        return dummy.next
```  

- 



-

### 哈希表 

### 二叉树  
- 相同 
```python 
# 如果p为空 或者 q为空
if not p or not q:
    return p is q 
# 相等的条件: p.val==q.val 且左右子树也相等 
return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right) 
```

- 对称 
```python 
class Solution:
    def isSymmetrical(self , pRoot: TreeNode) -> bool:
        # write code here 
        if not pRoot:
            return True  

        def helper(p: TreeNode, q:TreeNode):
            if not p or not q:
                return p is q 
            return p.val == q.val and helper(p.left, q.right) and helper(p.right, q.left)
        return helper(pRoot.left, pRoot.right) 
```

- 平衡 
```python 

```

- 右视图 
```python 

```

- 前序 
```python 
if not root:
    return []
cur = [(0, root)]
res = []
while cur:
    # 栈弹出, 实现后进先出
    flag, node = cur.pop() 
    if not node: continue 
    if flag == 0:
        # 因为后进先出, 故入栈反序  
        cur.append((0, node.right))
        cur.append((0, node.left))
        cur.append((1, node))  
    else:
        res.append(node.val) 
return res 
```

- 中序 
```python 
if not root:
    return []
cur = [(0, root)]
res = []
while cur:
    # 栈弹出, 实现后进先出
    flag, node = cur.pop() 
    if not node: continue 
    if flag == 0:
        # 因为后进先出, 故入栈反序  
        cur.append((0, node.right)) 
        cur.append((1, node)) 
        cur.append((0, node.left))
    else:
        res.append(node.val) 
return res 
```

- 后序  
```python 
if not root:
    return []
cur = [(0, root)]
res = []
while cur:
    # 栈弹出, 实现后进先出
    flag, node = cur.pop() 
    if not node: continue 
    if flag == 0:
        # 因为后进先出, 故入栈反序   
        cur.append((1, node)) 
        cur.append((0, node.right)) 
        cur.append((0, node.left))
    else:
        res.append(node.val) 
return res 
```

- 层序 
```python 
# 双数组解法 
if not root:
    return [] 
res = [] 
cur = [root] 
while cur:
    nxt = [] 
    vals = [] 
    # 遍历一层 
    for node in cur:
        vals.append(node.val) 
        if node.left: nxt.append(node.left) 
        if node.right: nxt.append(node.right) 
    cur = nxt 
    res.append(vals) 
return res

``` 

- 之字形(锯齿形)打印 
```python 
# 直接套用双数组解法 
class Solution:
    def Print(self , pRoot: TreeNode) -> List[List[int]]:
        # write code here 
        if not pRoot:
            return [] 
        res = [] 
        cur = [pRoot]  
        even = False 
        while cur:
            nxt = [] 
            vals = [] 
            # 遍历一层 
            for node in cur:
                vals.append(node.val) 
                if node.left: nxt.append(node.left) 
                if node.right: nxt.append(node.right) 
            cur = nxt 
            res.append(vals[::-1] if even else vals )  
            even = not even
        return res
```

- 最大深度  
```python 
class Solution:
    def maxDepth(self , root: TreeNode) -> int:
        # write code here 
        if not root:
            return 0 
        def dfs(node):
            if not node:
                return 0 
            l_dep = dfs(node.left)
            r_dep = dfs(node.right) 
            return max(l_dep, r_dep) + 1 
        return dfs(root)
```

- 是否平衡二叉树 
```python 
class Solution:
    def IsBalanced_Solution(self , pRoot: TreeNode) -> bool:
        # write code here 
        if not pRoot:
            return True 
        def get_height(root):
            if not root:
                return 0  
            left_dep = get_height(root.left) 
            if left_dep == -1:
                return -1 
            right_dep = get_height(root.right) 
            if right_dep == -1 or abs(left_dep - right_dep) > 1:
                return -1   
            return max(left_dep, right_dep) + 1
        return get_height(pRoot) != -1 
``` 

- 两个节点的最近公共祖先 
```python 
class Solution:
    def lowestCommonAncestor(self , root: TreeNode, o1: int, o2: int) -> int:
        # write code here 
        def dfs(root, o1, o2):
            if not root: return None 
            if root.val == o1 or root.val == o2:
                return root 
            left = dfs(root.left, o1, o2) 
            right = dfs(root.right, o1, o2)    
            if left and right:
                return root 
            if left: return left 
            return right 
            
            # if not left: return right 
            # if not right: return left 
            # return root 
        return dfs(root, o1, o2).val
``` 

- BST最近公共祖先  
```python 
class Solution:
    def lowestCommonAncestor(self , root: TreeNode, p: int, q: int) -> int:
        # write code here 
        def dfs(root, p, q):
            x = root.val 
            if x < p and x < q:
                return dfs(root.right, p, q) 
            if x > p and x > q:
                return dfs(root.left, p, q) 
            return root 
        return dfs(root, p, q).val
```

- 验证BST  
```python 
class Solution:
    pre = float('-inf')
    def isValidBST(self , root: TreeNode) -> bool:
        # write code here 
        # 中序遍历解法, 看当前节点值是否大于上一个节点值, 
        # 然后, 记录当前节点, 下一个值和它比较(重复上述步骤) 
        # pre = -inf 
        if not root:
            return True
        if not self.isValidBST(root.left) or root.val <= self.pre:
            return False 
        self.pre = root.val 
        return self.isValidBST(root.right) 
``` 

- BST与双向链表
```python 
class Solution:
    def Convert(self , pRootOfTree ):
        # write code here 
        if not pRootOfTree: 
            return None 
        self.arr = [] 
        self.midTraversal(pRootOfTree) 

        # 遍历最后数组最后一个元素之前的部分  
        for i, v in enumerate(self.arr[:-1]):
            v.right = self.arr[i+1] 
            self.arr[i+1].left = v   
        return self.arr[0] 

    # 中序遍历函数 
    def midTraversal(self, root):
        if not root:
            return 
        self.midTraversal(root.left) 
        self.arr.append(root)  
        self.midTraversal(root.right)   
```

### 回溯 

### 动态规划 

### 模拟 

### 二分查找  
- 寻找峰值
```python 

``` 

- 二分查找 
```python 

```

### 双指针 
- 合并区间
```python 
class Solution:
    def merge(self , intervals: List[Interval]) -> List[Interval]: 
        # write code here 
        if not intervals: return []  
        intervals = sorted(intervals, key = lambda x : x.start ) 
        res = [intervals[0]]  
        n = len(intervals) 
        for i in range(1, n): 
            if intervals[i].start <= res[-1].end:
                res[-1].end = max(res[-1].end, intervals[i].end) 
            else:
                res.append(intervals[i]) 
        return res 

```

- 两数之和  
```python 
class Solution:
    def merge(self , intervals: List[Interval]) -> List[Interval]: 
        # write code here 
        if not intervals: return []  
        intervals = sorted(intervals, key = lambda x : x.start ) 
        res = [intervals[0]]  
        n = len(intervals) 
        for i in range(1, n): 
            if intervals[i].start <= res[-1].end:
                res[-1].end = max(res[-1].end, intervals[i].end) 
            else:
                res.append(intervals[i]) 
        return res 

``` 

- 三数之和 
```python 
class Solution:
    def merge(self , intervals: List[Interval]) -> List[Interval]: 
        # write code here 
        if not intervals: return []  
        intervals = sorted(intervals, key = lambda x : x.start ) 
        res = [intervals[0]]  
        n = len(intervals) 
        for i in range(1, n): 
            if intervals[i].start <= res[-1].end:
                res[-1].end = max(res[-1].end, intervals[i].end) 
            else:
                res.append(intervals[i]) 
        return res 

``` 

- 无重复字符最长子串 
```python 
from collections import Counter
class Solution:
    def maxLength(self , arr: List[int]) -> int:
        # write code here 
        left = 0 
        res = 0 
        cnt = Counter() # hashmap of count of each char 
        for right, val in enumerate(arr):
            cnt[val] += 1
            while cnt[val] > 1:
                cnt[arr[left]] -= 1
                left += 1 
            res = max(res, right - left + 1) 
        return res 
``` 

- 最小覆盖子串 
```python  
class Solution:
    def minWindow(self , S: str, T: str) -> str:
        # write code here 
        from collections import Counter,defaultdict  
        need = Counter(T) 
        win = defaultdict(int)

        n = len(S) 
        left, right = 0, 0  
        start, length = 0, float('inf') 
        valid = 0  

        while right < n: 
            c = S[right] 
            right += 1
            if c in need:
                win[c] += 1
                if win[c] == need[c]:
                    valid += 1 

            while valid == len(need): 
                if right - left < length: 
                    start = left 
                    length = right - left  
                
                d = S[left]  
                left += 1
                if d in need: 
                    if win[d] == need[d]:
                        valid -= 1
                    win[d] -= 1 

        return "" if length == float('inf') else S[start : start + length] 


from collections import defaultdict, Counter 

need = Count(T) 
win = defaultdict() 
n = len(S) 
left, right = 0, 0 
valid = 0 
start, length = 0, float('inf') 

while right < n: 
    c = S[right] 
    right += 1 
    if c in need:
        win[c] += 1
        if win[c] == need[c]:
            valid += 1
    while valid == len(need):
        if right - left < length:
            start = left 
            length = right - left 
        
        d = s[left] 
        left += 1
        if d in need:
            if win[d] == need[d]:
                valid -= 1
            win[d] -= 1 
    return "" if length == float('inf') else S[start : start + lenght] 

```  

- 接雨水  
```python 
class Solution:
    def maxWater(self , arr: List[int]) -> int:
        # write code here 
        n = len(arr) 
        pre_max = suf_max = 0   
        left = 0  # 左指针
        right = n - 1  # 右指针
        ans = 0 
        while left < right:
            # 相向双指针移动, 更新 pre_max, suf_max 
            pre_max = max(pre_max, arr[left])
            suf_max = max(suf_max, arr[right])  
            # 若 pre_max 更小
            if pre_max < suf_max:  
                # 接的水 = 左侧最高板 - 当前高度
                ans += pre_max - arr[left]  
                # 左指针右移
                left += 1
            else: 
                # 接的水 = 右侧最高板 - 当前高度
                ans += suf_max - arr[right] 
                right -= 1
        return ans 
```  


- 盛最多水的容器  
```python 
class Solution:
    def maxArea(self , height: List[int]) -> int:
        # write code here 
        res = 0 
        left = 0  
        n = len(height) 
        right = n - 1 
        while left < right:
            area = (right - left) * min(height[left], height[right]) 
            res = max(res, area)  
            # 不断删掉矮的线, 直到相向双指针相遇 
            if height[left] < height[right]:
                left += 1 
            else:
                right -= 1 

        return res  
```  


### 单调栈 
- 每日温度  
```python 
# 从右到左遍历 
class Solution:
    def temperatures(self , dailyTemperatures: List[int]) -> List[int]:
        # write code here 
        n = len(dailyTemperatures) 
        res = [0] * n  
        s = []
        for i in range(n-1, -1, -1): 
            t = dailyTemperatures[i]   
            while s and t >= dailyTemperatures[s[-1]]: 
                s.pop() 
            if s:
                res[i] = s[-1] - i  # (栈顶元素下标 与 当前元素下标 的差)  
            s.append(i) 
        return res 
```  

- 

