# Assignment #1: 拉齐大家Python水平

Updated 0940 GMT+8 Feb 19, 2024

2023 fall, Complied by ==黄源森，工学院==



**说明：**

1）数算课程的先修课是计概，由于计概学习中可能使用了不同的编程语言，而数算课程要求Python语言，因此第一周作业练习Python编程。如果有同学坚持使用C/C++，也可以，但是建议也要会Python语言。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2

C/C++编程环境：Red Panda C++



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/



思路：(3min)



##### 代码

```python
# 
l=[0,1,1]
for _ in range(30):
    l.append(sum(l[-3:]))
print(l[int(input())])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240219204250177](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204250177.png)



### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A



思路：(5min)



##### 代码

```python
# 
import re

a=input()

pattern=re.compile(r'.*h.*e.*l.*l.*o.*')
b=re.search(pattern, a)
if b!=None:
    print('YES')
else:
    print('NO')
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240219204542885](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204542885.png)



### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A



思路：(4min)



##### 代码

```python
# 
a=input()
a=a.lower()
re=[]
for num in range(len(a)):
    if a[num]  not in ['i','a','e','o','u','y']:
        re.append(a[num])
for n in range(len(re)):
    print('.'+re[n],end='')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240219204615558](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204615558.png)



### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/



思路：(4min)



##### 代码

```python
# 
def f(i):
    if i==2:
        return 1
    for j in range(2,i):
        if i%j==0:
            return 0
    return 1
n=int(input())
for i in range(2,n//2+1):
    if f(i) and f(n-i):
        print(i,n-i)
        exit()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240219204353361](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204353361.png)



### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



思路：(5min)



##### 代码

```python
# 
s=list(input().split('+'))
al=[]
for u in s:
    t=len(u)
    c=u.find('n')
    if c!=0:
        xishu=int(u[:c])
    else:
        xishu=1
    mici=int(u[c+2:])
    if xishu!=0:
        al.append(mici)
print('n^%d'%max(al))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240219204423885](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204423885.png)



### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/



思路：(3min)



##### 代码

```python
# 
from collections import Counter
l=list(map(int,input().split()))
dic=Counter(l)
x=max(dic.values())
a=[]
for u in dic:
    if dic[u]==x:
        a.append(u)
print(*sorted(a))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240219204459043](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240219204459043.png)



## 2. 学习总结和收获

比较简单





