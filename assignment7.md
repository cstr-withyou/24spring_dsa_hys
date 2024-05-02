# Assignment #7: April 月考

Updated 1557 GMT+8 Apr 3, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2、



## 1. 题目

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



思路：



代码

```python
# 
l=list(input().split())
l.reverse()
print(' '.join(l))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240403205156649](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205156649.png)



### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



思路：



代码

```python
# 
from collections import defaultdict,deque
m,n=map(int,input().split())
l=list(map(int,input().split()))
d=defaultdict(int)
q=deque([])
t=0
c=0
for u in l:
    if u in d and d[u]!=0:
        continue
    else:
        if t==m:
            x=q.popleft()
            d[x] -= 1
            t-=1
        q.append(u)
        d[u]+=1
        t+=1

        c+=1
print(c)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240403205223234](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205223234.png)



### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：



代码

```python
# 
n,k=map(int,input().split())
l=list(map(int,input().split()))
l.sort()
if n==k:
    print(l[-1])
    exit()
if k==0:
    if l[0]==1:
        print(-1)
    else:
        print(l[0]-1)
    exit()
t=l[k-1]
if l[k]>t:
    print(t)
else:
    print(-1)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240403205249849](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205249849.png)



### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



思路：



代码

```python
# 
def dfs(x):
    if x>=2**n:
        if l[x-2**n]=='0':
            al[x]='B'
        else:
            al[x]='I'
    else:
        dfs(x+x)
        dfs(x+x+1)
        if al[2*x]==al[2*x+1]:
            al[x]=al[x+x]
        else:
            al[x]='F'
def d(x):
    if x>=2**n:
        return al[x]
    else:
        return d(2*x)+d(x+x+1)+al[x]
n=int(input())
l=input()
al=[0]*(2**(n+1))
dfs(1)
print(d(1))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240403205313587](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205313587.png)



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



思路：



代码

```python
# 
from collections import defaultdict
import queue

t = int(input())
l = []
dic = {}
now = set()
out = -1
q = queue.Queue()
flag = [queue.Queue() for _ in range(t)]
for _ in range(t):
    p = list(input().split())
    for u in p:
        dic[u] = _
    l.append(p)
while 1:
    s = input()
    if s == 'STOP':
        break
    if s[0] == 'D':
        if out != -1 and not(flag[out].empty()):
            print(flag[out].get())
        elif out == -1:
            out = q.get()
            print(flag[out].get())
        else:
            while (flag[out].empty()):
                now.remove(out)
                out = q.get()
            print(flag[out].get())
    else:
        a, b = s.split()
        g = dic[b]
        if g not in now:
            now.add(g)
            q.put(g)
            flag[g].put(b)
        else:
            flag[g].put(b)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240403205343869](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205343869.png)



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



思路：



代码

```python
# 
from collections import defaultdict
def dfs(x):
    res=[]
    u=dic[x]
    u.append(x)
    u.sort()
    for k in u:
        if k==x:
            res.append(x)
        else:
            res.extend(dfs(k))
    return res
n=int(input())
dic=defaultdict(list)
al=set()
v=set()
for i in range(n):
    p=list(map(int,input().split()))
    a=p[0]
    al.add(a)
    v.update(p[1:])
    dic[a]=p[1:]
t=al.difference(v)
u=0
for k in t:
    u=k
for k in dfs(u):
    print(k)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240403205408058](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240403205408058.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

手有点生疏了，但是这次发挥还是可以的，有些题目隐隐约约记得做过类似的，期中季过后再花一定时间在数算上，还要整理一下笔试。只不过做题不能急躁，最小整数已经知道了坑点在0和n上但还是改了半天。



