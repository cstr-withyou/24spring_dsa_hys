# Assignment #D: May月考

Updated 1654 GMT+8 May 8, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

环境：Spyder IDE 5.4.3



## 1. 题目

### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：



代码

```python
# 
L,M=map(int, input().split())
st=[]
num=0
for i in range(M):
    st.append(list(map(int, input().split())))
for m in range(L+1):
    for item in st:
        if item[0]<=m<=item[1]:
            num+=1
            break
        else:
            continue
print(L+1-num)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240514150303194](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150303194.png)



### 20449: 是否被5整除

http://cs101.openjudge.cn/practice/20449/



思路：



代码

```python
# 
s=input()
dp=[0]
for i in range(len(s)):
    dp.append((dp[-1]*2+int(s[i])))
ans=''
for u in dp[1:]:
    if u%5==0:
        ans+='1'
    else:
        ans+='0'
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240514150332664](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150332664.png)



### 01258: Agri-Net

http://cs101.openjudge.cn/practice/01258/



思路：



代码

```python
# 
import heapq

while 1:
    try:
        n = int(input())
        l = [list(map(int, input().split())) for _ in range(n)]
        vis = set([0])
        p = []
        al = 0
        for i in range(1, n):
            p.append((l[0][i], 0, i))
        heapq.heapify(p)
        while len(vis) < n:
            while 1:
                a, b, c = heapq.heappop(p)
                if not (b in vis and c in vis):
                    break
            al += a
            vis.add(c)
            for i in range(n):
                if i not in vis:
                    heapq.heappush(p, (l[c][i], c, i))
        print(al)

    except:
        break
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240514150356954](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150356954.png)



### 27635: 判断无向图是否连通有无回路(同23163)

http://cs101.openjudge.cn/practice/27635/



思路：



代码

```python
# 
def dfs(i):
    vis.add(i)
    for u in l[i]:
        if u not in vis:
            dfs(u)
def dfs2(i):
    for u in l[i]:
        if u not in vis:
            vis[u]=i
            if not dfs2(u):
                return 0
        elif u in vis and vis[i]!=u:
            return 0
    return 1
n,m=map(int,input().split())
l=[[]for _ in range(n)]
for _ in range(m):
    a,b=map(int,input().split())
    l[a].append(b)
    l[b].append(a)
vis=set()
dfs(0)
if len(vis)<n:
    print('connected:no')
else:
    print('connected:yes')
f=1
for i in range(n):
    vis={i:i}
    if not dfs2(i):
        f=0
        break
if f:
    print('loop:no')
else:
    print('loop:yes')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240514150422341](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150422341.png)





### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/



思路：



代码

```python
# 
import heapq
for _ in range(int(input())):
    p=list(map(int,input().split()))
    ans=[p[0]]
    l=[p[0]]
    r=[]
    t=len(p)
    for i in range(1,t):
        if len(l)>len(r):
            x=heapq.heappop(l)
            if p[i]<x:
                heapq.heappush(r, -p[i])
                heapq.heappush(l, x)
            else:
                heapq.heappush(r, -x)
                heapq.heappush(l, p[i])
        else:
            x=-heapq.heappop(r)
            if x>=p[i]:
                heapq.heappush(l, x)
                heapq.heappush(r, -p[i])
            else:
                heapq.heappush(l,p[i])
                heapq.heappush(r,-x )
            a=heapq.heappop(l)
            ans.append(a)
            heapq.heappush(l, a)
    print(len(ans))
    print(*ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240514150525844](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150525844.png)



### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/



思路：



代码

```python
# 
n=int(input())
l=[int(input()) for _ in range(n)]+[-1]
mi=[0]
dp1=[0]*n
dp2=[0]*n
ma=[0]
for i in range(1,1+n):
    while mi and l[i]>l[mi[-1]]:
        a=mi.pop()
    if i==n:
        break
    if mi:
        dp2[i]=mi[-1]
    else:
        dp2[i]=-1
    mi.append(i)
for i in range(1,1+n):
    while ma and l[i]<=l[ma[-1]]:
        a=ma.pop()
        dp1[a]=i
    ma.append(i)
ans=0

for i in range(n):
    t=dp1[i]
    for j in range(i+1,t):
        if dp2[j]<i:
            ans=max(ans,j-i+1)
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240514150504169](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240514150504169.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

动态中位数题考试没想出来，虽然看到heapq提示也没想到，菜还是得多练。。。奶牛排队要学习更好的nlgn算法

