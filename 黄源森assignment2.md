# Assignment #2: 编程练习

Updated 0953 GMT+8 Feb 24, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2

C/C++编程环境：Red Panda c++



## 1. 题目

### 27653: Fraction类

http://cs101.openjudge.cn/2024sp_routine/27653/



思路：



##### 代码

```python
# 
def gcd(m, n):
    """辗转相除法求最大公约数"""
    while m % n != 0:
        old_m = m
        old_n = n

        m = old_n
        n = old_m % old_n
    return n

class Fraction:
    def __init__(self, top, bottom):
        """初始化分数对象"""
        common = gcd(top, bottom)
        self.num = top // common
        self.den = bottom // common

    def __str__(self):
        """返回分数的字符串表示"""
        return f"{self.num}/{self.den}"

    def __add__(self, other):
        """分数加法运算"""
        new_num = self.num * other.den + self.den * other.num
        new_den = self.den * other.den
        common = gcd(new_num, new_den)
        return Fraction(new_num // common, new_den // common)

a,b,c,d=map(int,input().split())
fraction1 = Fraction(a,b)
fraction2 = Fraction(c,d)
result = fraction1 + fraction2

print(f"{result}")
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240227123555085](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123555085.png)



### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110



思路：



##### 代码

```
n,w=map(int,input().split())
l=[]
for _ in range(n):
     l.append(list(map(int,input().split())))
l.sort(key=lambda x:x[0]/x[1],reverse=1)
i=0
ans=0
while w>=0 and i<=n-1:
    if w>=l[i][1]:
        ans+=l[i][0]
        w-=l[i][1]
        i+=1
        
    else:
        t=l[i][0]/l[i][1]
        ans+=w*t
        break
print('%.1f'%ans)
```

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240227123504287](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123504287.png)



### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/



思路：



##### 代码

```python
# 
def f():
    global l,dic,b
    z=0
    for i in l:
        y=dic[i]
        y.sort(reverse=1)
        z+=sum(y[:m])
        if z>=b:
            return i
    return
for _ in range(int(input())):
    n,m,b=map(int,input().split())
    dic={}
    for __ in range(n):
        c,d=map(int,input().split())  
        dic[c]=dic.setdefault(c,[])+[d]
    l=list(dic.keys())
    l.sort()
    h=f()
    if h:
        print(h)
    else:
        print('alive')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227123622245](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123622245.png)



### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：



##### 代码

```python
# 
n=int(input())
def euler(p=10**6):
    global r
    i=3
    while i<p:
        if i in r:
            l=p//i
            for num in range(2,l+1):
                if num*i in r:
                    r-={num*i}
            i+=2
        else:
            i+=2
    return r

r=set([2,5]+[k for k in range(3,10**6,2) if str(k)[-1]!='5'])
c=euler()
from math import sqrt
def f(s):
    if s==4 or s==25:
        return 1
    if str(s)[-1] in ['2','3','7','6','4','0','5']:
        return 0
    if s==1:
        return 0
    t=s**0.5
    if int(t)!=t:
        return 0
    if t not in r:
        return 0
    return 1
l=list(map(int,input().split()))
for c in l:
    if f(c):
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227123711912](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123711912.png)



### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A



思路：



##### 代码

```python
# 
for _ in range(int(input())):
    n,x=map(int,input().split())
    ar=list(map(int,input().split()))
    start=0
    su=sum(ar)
    if su%x!=0:
        print(n)
    else:
       for start in range(n//2+1):
           if ar[start]%x!=0:
               break
       for end in range(n-1,n//2-1,-1):
           if ar[end]%x!=0:
               break
       if start==n//2  and end==n//2 :
           print(-1)
       else:
           print(max(n-start-1,end))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227123734188](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123734188.png)



### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：



##### 代码

```python
# 
def f(x):
    filter=[1 for i in range(x+1)]
    prime=[]
    for num in range(2,x+1):
        if filter[num]:
            prime.append(num)
        for p in prime:
            if num*p>x:
                break
            filter[num*p]=0
            if num*p==0:
                break
    return prime

p=f(10**4)
al=set()
for i in p:
    al.add(i*i)
m,n=map(int,input().split())    
for i in range(m):
    l=list(map(int,input().split()))
    t=len(l)
    ans=0
    for num in l:
        if num in al:
            ans+=num
    if ans==0:
        print(0)
    else:
        print('%.2f'%(ans/t))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227123801248](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240227123801248.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

计概都做过了，直接复制的hh。写点其他小组的题，比如数算A，程设



