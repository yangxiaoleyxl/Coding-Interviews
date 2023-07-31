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
