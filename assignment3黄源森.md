# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2



## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
# 
k=int(input())
l=list(map(int,input().split()))
dp=[1]*k
for i in range(1,k):

    for j in range(i):
        if l[i]<=l[j]:
            dp[i]=max(dp[i],dp[j]+1)
print(max(dp))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240306222031224](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222031224.png)



**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：



##### 代码

```python
# 
def f(a,b,c,d):
    if a==1:
        ans.append("1:"+b+'->'+d)
    else:
        f(a-1,b,d,c)
        ans.append(str(a)+':'+b+'->'+d)
        f(a-1,c,b,d)
a,b,c,d=input().split()
a=int(a)
ans=[]
f(a,b,c,d)
for u in ans:
    print(u)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240306222058287](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222058287.png)



**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：



##### 代码

```python
# 
while 1:
    n,p,m=map(int,input().split())
    if n==0:
        break
    ans=[]
    cur=p-1
    flag=[0]*n
    while len(ans)<n:
        c=0
        while c<m:
            if flag[cur]==0:
                c+=1
            cur=(cur+1)%n
        cur=(cur-1)%n
        flag[cur]=1
        ans.append(cur+1)
        cur=(cur+1)%n
    print(*ans,sep=',')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240306222122226](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222122226.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python
# 
k=int(input())
l=list(map(int,input().split()))
p=[]
for i in range(k):
    p.append((l[i],i+1))

p.sort()
for u in p:
    print(u[1],end=' ')
print()
ans=0
for i in range(k):
    u=p[i]
    ans+=u[0]*(k-i-1)

print('%.2f'%(ans/k))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240306222154698](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222154698.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
# 
def f(t,n):
    if n%2==1:
        return sorted(t)[(n-1)//2]
    else:
        return (sorted(t)[n//2]+sorted(t)[n//2-1])/2
n=int(input())
pairs = [i[1:-1] for i in input().split()]
h = [ sum(map(int,i.split(','))) for i in pairs]

p=list(map(int,input().split()))
l=[h[i]/p[i] for i in range(n)]
lm=f(l, n)
pm=f(p, n)
ans=0
for i in range(n):
    if l[i]>lm and p[i]<pm:
        ans+=1
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240306222239368](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222239368.png)



**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
# 
from collections import defaultdict
def f(x):
    a=float(x[:-1])
    b=x[-1]
    if b=="B":
        return a*1000000000
    else:
        return a*1000000
n=int(input())
dic=defaultdict(list)
for i in range(n):
    a,b=input().split('-')
    dic[a].append(b)
l=list(dic.keys())
for u in sorted(l):
    print(u,end=': ')
    s=dic[u]
    s.sort(key=lambda x:f(x))
    print(*s,sep=', ')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240306222302010](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240306222302010.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

难度其实一般，但是隔一段时间温习一些经典算法，有点温故而知新的感觉。虽然都做过，但是有点生疏的话反而容易掉坑。俗话说：“*拳不离手*,曲不离口”，代码也要不离手才能不断进步。



