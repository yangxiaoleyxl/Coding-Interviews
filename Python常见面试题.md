## Python Language Interview  


### 引用传递和值传递 
- Python中采取的是**传对象引用**的设计, 相当于**传值和传引用的综合**
- 传值还是传引用 <font color="red"> 取决于队对象属性 </font> , 如果是 immutable (Number, Tuple, String), 就是传值; 如果是 mutable (list, set, dict), 就是传引用
- 值传递, **函数内修改不影响函数外的对象**; 引用传递, **函数内修改会影响函数外的对象**

### @staticmethod 和 @classmethod 
- Python有3种方法, 静态方法(staicmethod), 类方法(classmethod) 和 实例方法 
```python 
# Python @staticmethod  @ classmethod 

class test:
    def method(self): 
        return 'instance method called', self 

    @classmethod 
    def classmethod(cls): 
        return 'class method called', cls 
    
    @staticmethod
    def staticmethod():
        return 'static method called' 
    
# Test these method in 'instance'
myClass = test() 

# instance method can call the instance 
print(myClass.method())

# No right to call instance  
print(myClass.classmethod())  

# No right to call class and instance 
print(myClass.staticmethod())  

# Test these method in 'Class' 
print(test.method(myClass))   
print(test.classmethod())   
print(test.staticmethod())   
``` 
这是用于区分三种方法的例子.可以看到**实例方法可以访问类和实例**. **类方法可以访问类,但不能访问实例**, **静态方法既不能访问对象实例状态也不能访问类状态**  

### sort() 和 sorted()  
- sort() 是list的方法,只能由 list 调用, **不反悔任何值且改变原始list**
- sorted() 是一个可对 sequence, list, set 和 dict 按升序或降序方法排序的方法,返回一个list 
```python 
# Python program to demonstrate
# sorted()


# List
x = ['q', 'w', 'r', 'e', 't', 'y']
print(sorted(x))

# Tuple
x = ('q', 'w', 'e', 'r', 't', 'y')
print(sorted(x))

# String-sorted based on ASCII translations
x = "python"
print(sorted(x))

# Dictionary
x = {'q': 1, 'w': 2, 'e': 3, 'r': 4, 't': 5, 'y': 6}
print(sorted(x))

# Set
x = {'q', 'w', 'e', 'r', 't', 'y'}
print(sorted(x))
```

