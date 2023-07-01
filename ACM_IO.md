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
num = int(input()) 
for i in range(num):
    a = input().split() 
    print(sum(list(map(int, a[1::]))))
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




