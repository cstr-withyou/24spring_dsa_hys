# Assignment #B: 图论和树算

Updated 1709 GMT+8 Apr 28, 2024

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

### 28170: 算鹰

dfs, http://cs101.openjudge.cn/practice/28170/



思路：



代码

```c++
# 
#include<iostream>
#include<algorithm>
#include<string.h>
using namespace std;
string l[10];
int flag[10][10];
void dfs(int i,int j){
	if(i>=1 and flag[i-1][j]==0 and l[i-1][j]=='.'){
		flag[i-1][j]=1;
		dfs(i-1,j);
	}
	if(j>=1 and flag[i][j-1]==0 and l[i][j-1]=='.'){
		flag[i][j-1]=1;
		dfs(i,j-1);
	}
	if(i<9 and flag[i+1][j]==0 and l[i+1][j]=='.'){
		flag[i+1][j]=1;
		dfs(i+1,j);
	}
	if(j<9 and flag[i][j+1]==0 and l[i][j+1]=='.'){
		flag[i][j+1]=1;
		dfs(i,j+1);
	}
}
int main(){
	for(int i=0;i<10;i++){
		cin>>l[i];
	}
	int c=0;
	memset(flag,0,sizeof(int)*100);
	for(int i=0;i<10;i++){
		for(int j=0;j<10;j++){
			if(l[i][j]=='.' and flag[i][j]==0){
				flag[i][j]=1;
				dfs(i,j);
				c++;
			}
		}
	}
	cout<<c;
}
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240430213125739](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213125739.png)



### 02754: 八皇后

dfs, http://cs101.openjudge.cn/practice/02754/



思路：



代码

```python
# 
def c(u,l):
    t=len(l)
    for i in range(len(l)):
        if l[i]==u or abs(t-i)==abs(u-l[i]):
            return 0
    return 1
al=[] 
def dfs(i,l):
    if i==8:
        al.append(l)
    for u in range(1,9):
        if c(u, l):
            dfs(i+1,l+[u])
dfs(0,[])
for _ in range(int(input())):
    ans=''
    for u in al[int(input())-1]:
        ans+=str(u)
    print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240430213150464](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213150464.png)



### 03151: Pots

bfs, http://cs101.openjudge.cn/practice/03151/



思路：



代码

```python
# 
from collections import deque,defaultdict
a,b,c=map(int,input().split())
q=deque([(0,0)])
dic={}
dic[(0,0)]=None
while q:
    x,y=q.popleft()
    if x==c or y==c:
        ans=[]
        while dic[(x,y)]!=None:
            ans.append(dic[(x,y)][2])
            x,y=dic[(x,y)][0],dic[(x,y)][1]
        print(len(ans))
        for u in reversed(ans):
            print(u)
        exit()
    if (a,y) not in dic:
        q.append((a,y))
        dic[(a,y)]=(x,y,'FILL(1)')
    if (x,b) not in dic:
        q.append((x,b))
        dic[(x,b)]=(x,y,'FILL(2)')
    if (0,y) not in dic:
        q.append((0,y))
        dic[(0,y)]=(x,y,'DROP(1)')
    if (x,0) not in dic:
        q.append((x,0))
        dic[(x,0)]=(x,y,'DROP(2)')
    if  x>b-y and (x-b+y,b) not in dic:
        q.append((x-b+y,b))
        dic[(x-b+y,b)]=(x,y,'POUR(1,2)')
    if x<=b-y and (0,x+y) not in dic:
        q.append((0,x+y))
        dic[(0,x+y)]=(x,y,'POUR(1,2)')
    if y>a-x and (a,y+x-a) not in dic:
        q.append((a,y+x-a))
        dic[(a,y+x-a)]=(x,y,'POUR(2,1)')
    if y<=a-x and (x+y,0) not in dic:
        q.append((x+y,0))
        dic[(x+y,0)]=(x,y,'POUR(2,1)')
print('impossible')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240430213219451](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213219451.png)



### 05907: 二叉树的操作

http://cs101.openjudge.cn/practice/05907/



思路：



代码

```python
# 
from collections import deque
class Node:
    def __init__(self,val):
        self.val=val
        self.left=None
        self.right=None
class Tree:
    def __init__(self):
        self.root=Node(0)
    def dfs_insert(self,x):
        global dic
        b,c=dic[x.val]
        if b!=-1:
            x.left=Node(b)
            self.dfs_insert(x.left)
        if c!=-1:
            x.right=Node(c)
            self.dfs_insert(x.right)
    def search(self,a):
        q=deque([self.root])
        while q:
            x=q.popleft()
            if x.left:
                if x.left.val==a:
                    return x
                q.append(x.left)
            if x.right:
                if x.right.val==a:
                    return x
                q.append(x.right)
    def type2(self,a):
        if a==0:
            x=self.root
        else:
            x=self.search(a)
            if x.right.val==a:
                x=x.right
        while 1:
            if x.left==None:
                return x.val
            else:
                x=x.left
    def type1(self,a,b):
        xa,xb=self.search(a),self.search(b)
        flag=[0,0]
        if xa.right.val==a:
            flag[0]=1
        if xb.right.val==b:
            flag[1]=1 
        if flag==[0,0]:
            xa.left,xb.left=xb.left,xa.left
        elif flag==[0,1]:
            xa.left,xb.right=xb.right,xa.left
        elif flag==[1,0]:
            xa.right,xb.left=xb.left,xa.right
        else:
            xa.right,xb.right=xb.right,xa.right
        return
    
    
for _ in range(int(input())):
    m,n=map(int,input().split())
    dic={}
    for i in range(m):
        a,b,c=map(int,input().split())
        dic[a]=(b,c)
    s=Tree()
    s.dfs_insert(s.root)
    for i in range(n):
        t=list(input().split())
        if t[0]=='1':
            a,b=int(t[1]),int(t[2])
            s.type1(a, b)
        else:
            a=int(t[1])
            print(s.type2(a))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240430213346744](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213346744.png)





### 18250: 冰阔落 I

Disjoint set, http://cs101.openjudge.cn/practice/18250/



思路：



代码

```python
# 
def f(x):
    while dic[x]!=x:
        x=dic[x]
    return x
while 1:
    try:
        n,m=map(int,input().split())
        dic={}
        for i in range(1,n+1):
            dic[i]=i
        for _ in range(m):
            x,y=map(int,input().split())
            a=f(x)
            b=f(y)
            if a==b:
                print('Yes')
            else:
                dic[b]=a
                dic[x]=a
                dic[y]=a
                print('No')
        res=[]
        for i in range(1,n+1):
            if f(i)==i:
                res.append(i)
        print(len(res))
        print(*res)
    except:
        break
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240430213430242](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213430242.png)



### 05443: 兔子与樱花

http://cs101.openjudge.cn/practice/05443/



思路：



代码

```python
# 
from collections import defaultdict
import heapq
dic=defaultdict(list)
p=int(input())
l=[input() for _ in range(p)]
q=int(input())
for _ in range(q):
    a,b,c=input().split()
    c=int(c)
    dic[a].append((c,a,b))
    dic[b].append((c,b,a))
for _ in range(int(input())):
    s,e=input().split()
    if s==e:
        print(s)
        continue
    u=dic[s]
    heapq.heapify(u)
    vis=set([s])
    par={}
    while 1:
        while 1:
            x,y,z=heapq.heappop(u)
            if z not in vis:
                break
        vis.add(z)
        par[z]=(y,x)
        if z==e:
            al=[]
            break
        for k in dic[z]:
            n,m,h=k
            heapq.heappush(u,(n+x,z,h))
    cur=e
    while 1:
        a,b=par[cur]
        al.append((cur,b))
        if a==s:
            break
        cur=a
    al.reverse()
    al=[(s,0)]+al
    ans=s
    for i in range(1,len(al)):
        a,b=al[i-1]
        x,y=al[i]
        ans+='->('+str(y-b)+')->'+x
    print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240430213515035](C:\Users\huawei\AppData\Roaming\Typora\typora-user-images\image-20240430213515035.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

五一时间多一些，把类似走山路的这种题多练一点，笔试内容也要花一点时间复习



