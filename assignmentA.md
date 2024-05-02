# Assignment #A: 图论：遍历，树算及栈

Updated 2018 GMT+8 Apr 21, 2024

2024 spring, Complied by ==黄源森，工学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：W11

Python编程环境：Spyder IDE 5.2.2

## 1. 题目

### 20743: 整人的提词本

http://cs101.openjudge.cn/practice/20743/



思路：



代码

```c++
# 
#include<iostream>
#include <algorithm>
#include <string>
using namespace std;
string f(string s){
	auto t=s.find(')');
	if (t==s.npos) return s;
	int x;
	for(int i=t-1;i>=0;i--){
		if (s[i]=='(') {
			x=i;
			break;
		}
	}
	string ans=s.substr(0,x);
	for(int i=t-1;i>x;i--){
		ans+=s[i];
	}
	ans+=s.substr(t+1);
	return f(ans);
}
int main(){
	string s;
	cin>>s;
	cout<<f(s);
}
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240423172814092](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423172814092.png)



### 02255: 重建二叉树

http://cs101.openjudge.cn/practice/02255/



思路：



代码

```python
# 
def f(x,y):
    if len(x)==0:
        return ''
    if len(x)==1:
        return x
    
    a=x[0]
    s=y.index(a)
    return f(x[1:1+s],y[:s])+f(x[1+s:],y[s+1:])+a
while 1:
    try:
        x,y=input().split()
        print(f(x, y))
    except:
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240423172848920](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423172848920.png)



### 01426: Find The Multiple

http://cs101.openjudge.cn/practice/01426/

要求用bfs实现



思路：



代码

```python
# 
from collections import deque
def f(n):
    if n == 1:
        return 1
    q= deque([10,11])
    l =[1]
    while q: 
        a=q.popleft()
        t=a%n
        if t == 0:
            return str(a)
        else:
            if t not in l: 
                l.append(t)
                q.append(a*10+1)
                q.append(a*10)
while True: 
    n = int(input()) 
    if n ==0 : 
        break
    else:
        print(f(n))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423214346054](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423214346054.png)



### 04115: 鸣人和佐助

bfs, http://cs101.openjudge.cn/practice/04115/



思路：



代码

```python
# 
def f():
    global x,mr,zz
    while not x.empty():
        s=x.get()
        ne=[]
        for step in nextstep:
            r=[s[0]+step[0],s[1]+step[1]]
            if (r[0],r[1],s[2]-[0,1][k[r[0]][r[1]]=='#']) in flag:
                continue
            if k[r[0]][r[1]]==-1:
                continue
            elif k[r[0]][r[1]]=='+':
                return s[3]+1
            elif k[r[0]][r[1]]=='#':
                if s[2]>0:
                    x.put((r[0],r[1],s[2]-1,s[3]+1))
                    flag.add((r[0],r[1],s[2]-1))
            else:
                x.put((r[0],r[1],s[2],s[3]+1))
                flag.add((r[0],r[1],s[2]))
    return -1
import queue
m,n,t=map(int,input().split())
k=[[-1]*(n+2)]
mr=-1
flag=set()
nextstep=[[-1,0],[1,0],[0,-1],[0,1]]
for _ in range(m):
    kk=[-1]+list(input())+[-1]
    k.append(kk)
    if mr==-1:
        try:
           mr=kk.index('@')
           mr=(_+1,mr,t,0)
           
        except:
            continue
k.append([-1]*(n+2))
x=queue.Queue()
x.put(mr)
flag.add(mr[:3])
print(f())
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423172933597](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423172933597.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/



思路：



代码

```python
# 
from collections import deque
def f(a,b,c,d):
    if a==c and b==d:
        return 0
    if l[a][b]=='#' or l[c][d]=='#':
        return 'NO'
    q=deque([(a,b,0)])
    while len(q)>0:
        x,y,z=q.popleft()
        if z>flag[x][y]:
            continue
        for step in [(x-1,y),(x+1,y),(x,y-1),(x,y+1)]:
            h,w=step
            if 0<=h<m and 0<=w<n and l[h][w]!='#' and flag[h][w]>z+abs(int(l[x][y])-int(l[h][w])) :
                flag[h][w]=z+abs(int(l[x][y])-int(l[h][w]))
                q.append((h,w,z+abs(int(l[x][y])-int(l[h][w]))))
    if flag[c][d]==float('inf'):
        return 'NO'
    else:
        return flag[c][d]
m,n,p=map(int,input().split())
l=[list(input().split()) for _ in range(m)]
for _ in range(p):
    flag=[[float('inf')]*n for _ in range(m)]
    a,b,c,d=map(int,input().split())
    print(f(a, b, c, d))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423173019456](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423173019456.png)



### 05442: 兔子与星空

Prim, http://cs101.openjudge.cn/practice/05442/



思路：



代码

```python
# 
import heapq
from collections import defaultdict
n=int(input())
dc=defaultdict(list)
for _ in range(n-1):
    s=list(input().split())
    a=s[0]
    b=int(s[1])
    t=[]
    for i in range(b):
        c,d=s[2+2*i],s[3+2*i]
        d=int(d)
        dc[a].append((d,a,c))
        dc[c].append((d,c,a))
p=set(['A'])
f=dc['A']
ans=0
c=1
heapq.heapify(f)
while c<n:
    while 1:
        a=heapq.heappop(f)
        if not (a[1] in p and a[2] in p):
            if a[1] in p:
                r=a[2]
            else:
                r=a[1]
            p.add(r)
            ans+=a[0]
            c+=1
            for u in dc[r]:
                heapq.heappush(f, u)
            break
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423173102944](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240423173102944.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

最近已经增大了一些刷题量，五一再接再厉！只不过以前写过的算法还要多加温习



