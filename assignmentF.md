# Assignment #F: All-Killed 满分

Updated 1844 GMT+8 May 20, 2024

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

### 22485: 升空的焰火，从侧面看

http://cs101.openjudge.cn/practice/22485/



思路：



代码

```python
# 
def dfs(i,k):
    t[k]=i
    for u in l[i-1]:
        if u==-1:
            continue
        dfs(u,k+1)
n=int(input())
l=[list(map(int,input().split())) for _ in range(n)]
t=[-1]*1000
dfs(1,0)
for u in t:
    if u!=-1:
        print(u,end=' ')
    else:
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240521201820201](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521201820201.png)



### 28203:【模板】单调栈

http://cs101.openjudge.cn/practice/28203/



思路：



代码

```python
# 
n=int(input())
l=list(map(int,input().split()))
s=[]
p=[0]*n
for i in range(n):
    if not s:
        s.append(i)
    else:
        while s and l[i]>l[s[-1]]:
            t=s.pop()
            p[t]=i+1
        s.append(i)
print(*p)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240521202931649](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521202931649.png)



### 09202: 舰队、海域出击！

http://cs101.openjudge.cn/practice/09202/



思路：



代码

```python
# 
from collections import defaultdict,deque
for _ in range(int(input())):
    n,m=map(int,input().split())
    dic=defaultdict(list)
    dg=defaultdict(int)
    for _ in range(m):
        x,y=map(int,input().split())
        dic[x].append(y)
        dg[y]+=1
    q=deque([])
    vis=set()
    for i in range(1,m+1):
        if dg[i]==0:
            q.append((i))
            vis.add(i)
    f=0
    
    while q:
        a=q.popleft()
        for u in dic[a]:
            if u in vis:
                continue
            dg[u]-=1
            if dg[u]==0 and u not in vis:
                q.append(u)
                vis.add(u)

    for i in range(1,n+1):
        if dg[i]>0:
            f=1
    if f:
        print('Yes')
    else:
        print('No')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521201853702](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521201853702.png)



### 04135: 月度开销

http://cs101.openjudge.cn/practice/04135/



思路：



代码

```python
# 
def f(mid):
    cur=0
    al=0
    for i in range(n):
        if cur+p[i]>mid and cur<=mid:
            al+=1
            cur=p[i]
        else:
            cur+=p[i]
    return al+1
n,m=map(int,input().split())
p=[int(input()) for _ in range(n)]
l,r=max(p),sum(p)
while r-l>1:
    mid=(l+r)//2
    if f(mid)<=m:
        r=mid
    else:
        l=mid
if f(l)>m:
    print(r)
else:
    print(l)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521201925900](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521201925900.png)



### 07735: 道路

http://cs101.openjudge.cn/practice/07735/



思路：



代码

```c++
# 
#include<iostream>
#include<queue>
#include<map>
#include<limits>
using namespace std;
const int INF=numeric_limits<int>::max();
struct road{
	int l,t,d;
};
struct node{
	int l,t;
	int pos;
	bool operator < (const node a)const	{
		return l<a.l;
	}
};
int main(){
	int k,n,r;
	cin>>k>>n>>r;
	int h[n+1][k+1];
   for (int i=0;i<n+1;i++){
       for(int j=0;j<k+1;j++){
           h[i][j]=INF;
       }
   }
	map<int,vector<road>> dic;
	for(int i=0;i<r;i++){
		int s,d,l,t;
		cin>>s>>d>>l>>t;
		road a{l,t,d};
		dic[s].push_back(a);
	}
	priority_queue<node> q;
	if(dic.count(1)){
		vector<road> p=dic[1];
		int t=p.size();
		for(int i=0;i<t;i++){
			node a{p[i].l,p[i].t,p[i].d};
			q.push(a);
		}
	}
	else{
		cout<<-1<<endl;
		return 0;
	}
	while(not q.empty()){
		node x=q.top();
		q.pop();
		if(x.t<=k && h[x.pos][x.t]>x.l){
			for(int i=x.t;i<k+1;i++){
				h[x.pos][i]=min(h[x.pos][i],x.l);
			}
			if(dic.count(x.pos)){
				vector<road> p=dic[x.pos];
				int u=p.size();
				for(int j=0;j<u;j++){
              if(p[j].t+x.t<=k && h[p[j].d][p[j].t+x.t]>p[j].l+x.l){
					node xx{p[j].l+x.l,p[j].t+x.t,p[j].d};
					q.push(xx);
				}
                }
			}
		}
	}
	if(h[n][k]==INF) cout<<-1;
	else cout<<h[n][k];
}
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521202032723](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521202032723.png)



### 01182: 食物链

http://cs101.openjudge.cn/practice/01182/



思路：



代码

```python
# 
def f(x):
    t=0
    while x!=dic[x][0]:
        t+=dic[x][1]
        t=t%3
        x=dic[x][0]
    return x,t
            
n,k=map(int,input().split())
d=0
dic={}
for i in range(1,n+1):
    dic[i]=(i,0)
for _ in range(k):
    a,b,c=map(int,input().split())
    if a==1:
        if b>n or c>n:
            d+=1
        else:
            x1,t1=f(b)
            x2,t2=f(c)
            if x1==x2:
                if t1!=t2:
                    d+=1 
                    #print(_)
            else:
                dic[x2]=(x1,(t1-t2)%3)
    else:
        if b>n or c>n:
            d+=1
        else:
            x1,t1=f(b)
            x2,t2=f(c)
            if x1==x2:
                if t1-t2 not in {-1,2}:
                    d+=1 
                    #print(_)
            else:
                dic[x2]=(x1,(t1-t2+1)%3)
    #print(dic)
print(d)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521202106834](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240521202106834.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

roads是老题了，单调栈就是找比它大的用单调递减栈，比它小的单增（无论左右）

