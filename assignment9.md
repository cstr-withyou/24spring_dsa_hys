# Assignment #9: 图论：遍历，及 树算

Updated 1739 GMT+8 Apr 14, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2, 



## 1. 题目

### 04081: 树的转换

http://cs101.openjudge.cn/dsapre/04081/



思路：



代码

```python
# 
s=input()
flag=[0]*10002
r,t,h=0,0,0
for u in s:
    if u=='u':
        r-=1
        flag[r]+=1
    else:
        r+=1
        flag[r]=flag[r-1]+1
        t=max(r,t)
        h=max(h,flag[r])
print(f'{t} => {h}')
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240415125741257](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415125741257.png)



### 08581: 扩展二叉树

http://cs101.openjudge.cn/dsapre/08581/



思路：



代码

```python
# 
class Node:
    def __init__(self,v,p):
        self.val=v
        self.left=None
        self.right=None
        self.par=p
class Tree:
    def __init__(self,v):
        self.root=Node(v, None)
    def struct(self,s):
        cur=self.root
        for u in s[1:]:
            if cur.left==None:
                cur.left=Node(u,cur)
                if u!='.':
                    cur=cur.left
            elif cur.right==None:
                cur.right=Node(u,cur)
                if u=='.':
                    while cur!=None and cur.right!=None:
                        cur=cur.par
                else:
                    cur=cur.right
          #  print(cur.val,u)
    def f(self,x):
        if x.val=='.':
            return ''
        return self.f(x.left)+x.val+self.f(x.right)
    def g(self,x):
        if x.val=='.':
            return ''
        return self.g(x.left)+self.g(x.right)+x.val
s=input()
t=Tree(s[0])
t.struct(s)
print(t.f(t.root))
print(t.g(t.root))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240415125835314](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415125835314.png)



### 22067: 快速堆猪

http://cs101.openjudge.cn/practice/22067/



思路：



代码

```c++
# 
#include <string>
#include <stack>
#include <iostream>
#include <vector>
using namespace std;

int main() {
    string s;
    stack<int> a;
    vector<int> m;
    
    while (cin >> s) {
        if (s == "pop") {
            if (!a.empty()) {
                a.pop();
                if (!m.empty()) m.pop_back(); 
            }
        } else if (s == "min") {
            if (!m.empty()) cout << m.back() << endl;
        } else {
            int h;
            cin >> h;
            a.push(h);
            if (m.empty()) m.push_back(h); 
            else {
                int k = m.back();
                m.push_back(min(k, h));
            }
        }
    }

    return 0;
}
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240415125931584](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415125931584.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123



思路：



代码

```python
# 
exec('''import sys
sys.setrecursionlimit(200000)
def dfs(i,j,k):
    global ans
    if k==0:
        ans+=1
        return
    for step in steps:
        a,b=i+step[0],j+step[1]
        if 0<=a<m and 0<=b<n and flag[a][b]:
            flag[a][b]=0
            dfs(a,b,k-1)
            flag[a][b]=1
    
    
steps=[[-2,-1],[-1,-2],[1,2],[2,1],[-1,2],[-2,1],[1,-2],[2,-1]]    
for _ in range(int(input())):
    n,m,x,y=map(int,input().split())
    flag=[[1]*n for __ in range(m)]
    ans=0
    flag[y][x]=0
    dfs(y,x,m*n-1)
    print(ans)''')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240415130022234](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415130022234.png)



### 28046: 词梯

bfs, http://cs101.openjudge.cn/practice/28046/



思路：



代码

```python
# 
from collections import deque
def ff(x,y):
    t=len(x)
    c=0
    for i in range(t):
        if x[i]!=y[i]:
            c+=1
            if c>1:
                return 0
    return 1
n=int(input())
l=list(input() for _ in range(n))
a,b=input().split()
q=deque()
q.append(a)
dic={}
while q:
    f=0
    x=q.popleft()
    if x==b:
        break
    for u in l:
        if u not in dic and ff(x,u):
            q.append(u)
            dic[u]=x
            if u==b:
                f=1
                break
    if f:
        break
s=[b]
cur=b
while cur!=a:
    if cur not in dic:
        print("NO")
        exit()
    cur=dic[cur]
    s.append(cur)
print(*reversed(s))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240415130055866](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415130055866.png)



### 28050: 骑士周游

dfs, http://cs101.openjudge.cn/practice/28050/



思路：



代码

```python
# 
from collections import deque
def f(a,b):
    al=0
    for u in [(a-1,b-2),(a-2,b-1),(a+2,b+1),(a+1,b+2),(a-1,b+2),(a-2,b+1),(a+2,b-1),(a+1,b-2)]:
        c,d=u
        if 0<=c<n and 0<=d<n and (c,d) not in vis:
            al+=1
    return al
def g(a,b):
    res=aa,bb
    t=1e9
    for u in [(a-1,b-2),(a-2,b-1),(a+2,b+1),(a+1,b+2),(a-1,b+2),(a-2,b+1),(a+2,b-1),(a+1,b-2)]:
        c,d=u
        if 0<=c<n and 0<=d<n and (c,d) not in vis:
            k=f(u[0],u[1])
            if k<t:
                res=u
                t=k
    return res
n=int(input())
aa,bb=map(int,input().split())
q=deque()
vis=set([(aa,bb)])
q.append((aa,bb))
c=1
while q:
    p,m=q.popleft()
    nx=g(p,m)
    if nx==(aa,bb):
        print('fail')
        exit()
    vis.add(nx)
    q.append(nx)
    c+=1
    if c==n**2:
        print('success')
        exit()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240415130128651](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240415130128651.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

有些题目应该多用不同方法解，图的题要注意细节

