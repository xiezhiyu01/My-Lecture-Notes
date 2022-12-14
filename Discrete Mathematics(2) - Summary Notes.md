### 离散复习 by xzy



#### chapter1 基本概念

简单图：无重边、自环

邻接矩阵：可以表示自环，不能表示重边。（第i行第j列为1表示有 $ v_{i} $  到 $ v_{j} $ 的边)

权矩阵：同上

关联矩阵：行为点，列为边，一列一个1一个-1区别出入度。可以表示重边，不能表示自环。

边列表：三个数组ABC，相同下标分别储存起点、终点和权值

正向表：见PPT （A是n+1维，有向图的B是m、无向图的B是2m）

邻接表：略



#### chapter2 道路与回路

简单有向道路：边不重复

初级有向道路：点不重复

有向图的连通性<span style=color:blue>不考虑</span>方向！！

极大连通子图（不是G任何连通子图的真子图） = 连通支  ---> 都是G的导出子图

##### 欧拉回路：经过所有边的简单回路

<u>Thm.</u>无向<span style=color:blue>连通图</span>G存在欧拉回路的充要条件：G中各个节点的度都是偶数。

两个度为奇的节点 --> 存在欧拉道路 （证明：把两个点连起来）

有向连通图 --> 正、负度相等

##### 哈密顿回路：经过所有点的初级回路

重边和自环不影响H回路，所以一般对简单图研究H回路。

<u>Thm.</u>简单图G中任意两点度数和>=n-1,则G中存在哈密顿**道路**。

<u>Col.</u>简单图G中任意两点度数和>=n,则G中存在哈密顿**回路**。

若有道路没有回路，则道路两端点的度数之和<=n-1

<u>Col.</u>简单图G中两**不相邻**节点i、j，若度数之和>=n,则G有H回路<=>G+e(i,j)有H回路

把满足条件的i和j连起来，最后得到<span style=color:blue>闭合图</span>C(G)   ----> 闭合图唯一！

##### 旅行商问题：在正权完全图中求最短H回路

1、暴搜+剪枝

2、“便宜”算法：一开始是只有V1一个点的自环，每次选离环最近的一个点，这个点有两种方式插到环中，选比较短的那一种，重复操作。（可以证明，当满足三角不等式时，此算法解<2*最优解）

##### 最短路径

正权图 Dijkstra ：每次找到离永久标记集合最近的点，把它永久标记并更新它的后继，重复操作。

正确性？

有负权可用Ford：每次都对所有点i更新（用i的所有前继点j更新它） O(mn)

##### 关键路径

PT图：节点表示工序，有向边表示次序关旭，边权表示时长

PERT图：有向边表示工序，权值表示时间



#### Chapter3 树

<u>Def.</u>不含回路的连通图是树，用T表示。

<u>Def.</u>割边：去掉它之后连通支数增加 ---> 当且仅当e不属于G的任何回路

<u>Def.</u>基本关联矩阵：将关联矩阵任意划去一行，满秩（proof. P40）

prufer还没看！！

##### 有向连通图的支撑树计数：Binet-Cauchy定理

A 扁矩阵$m*n$     B 高矩阵 $n*m$   

$ det(AB) = \Sigma_{i}A_iB_i $ （A取m列的行列式*B取对应m行的行列式）

$B_k$是有向**连通图**G=（V,E）的基本关联矩阵，则G的不同支撑树的数目：$det(B_kB_k^T)$

$B_kB_k^T$ 其实就是：第i个对角线是i的度数，其余是负的$(v_i,v_j)$或者反过来边的边数

注意：这里求的都不是根树！！！边的方向完全不用考虑的！！但是在理论上B_k是定向的，不过到乘起来之后就没有区分了。

一定不含某边：简单；一定含某边：可以缩点

##### 有向连通图的根树计数

<u>Def</u>. 一棵树，一个节点的负度为0，其余的负度为1。T为外向树（或根树），用$\vec{T}$表示

$\vec{B_k}$表示把所有1改成0

以k为根的根树数目：$det(\vec{B_k}B_k^T)$

一定不含某边：简单；一定含(u,v)边：不能缩点（防止到v再到u再往下），要把其他所有以v为终点的边删掉

##### 回路矩阵

完全回路矩阵：$C_e$ 每行一个回路，每列代表一条边，行里1表示方向同，-1表示方向不同 

（前提：有向连通图！！！）

基本回路矩阵：$C_f$ G的支撑树T确定后，每条余树边对应的回路称为基本回路，方向与它一致

$C_f = ( I , C_{f_{12}} )$ 右边是树枝边对应的子阵

rank =  m - n +1

Thm.  $BC_e^T =0$ （边次序要一致）

col. $B_kC_f^T =0$

看第47面，C_e的rank也是m-n+1

- $C_{f_{12}}=-B_{11}^T*(B_{12}^{-1})^T$
- $C_e$完全回路矩阵的秩为m-n+1 (用C_k和B夹)
- (m-n+1)个互相独立的回路组成的矩阵是G的回路矩阵C
- C_f是回路矩阵，BC^T=0，C=P*C_f，P可逆
- 回路矩阵C的任意一个(m-n+1)阶子阵行列式非零<=>列对应G一余树
- 基本关联矩阵的任意一个n-1阶子阵行列式非零<=>列对应G一支撑树
- 割集矩阵S的任意一个(n-1)阶子阵行列式非零<=>列对应G一支撑树

##### 割集矩阵

割集的定义：S是有向图G的边子集，如果去掉S后G的连通支数多1、S的子集不能达到这样效果，则S是G的一个割集。

S定方向---> 有向割集

- 完全割集矩阵$S_e$
- 基本割集&基本割集矩阵$S_f$
- S_f的秩是n-1，$S_f = (S_{f_{11}}, I )$
- $S_eC_e^T =0$
- n-1个互相独立的割集组成的矩阵是G的割集矩阵S
- S_f是割集矩阵，SC^T=0，S=P*S_f，P可逆
- 对应关系（见上）
- $S_f=(S_{f_{11}},I)$    $C_f=(I,C_{f_{12}})$
- $S_{f_{11}} = -C_{f_{12}}^T$

##### 支撑树的生成

dis(t1,t2) = k （t1一共有k条边不属于t2）两棵树的距离是k

def 基本树变换

两距离为1的树，t1-t2=(e),t2-t1=(b)，则$b\in S_e(t1)$;反之，如果$b\in S_e(t1)$，则t1-e+b是一棵树

$T^e$表示对G的某颗树$t_0$和其中一条边e，与t_0距离为1且用一条边（实际上属于割集）替代e的新树集合

G中与t_0距离为1的树一定恰在T^e1,T^e2.....中的一个集合里！！！

##### Huffman树

WPL = sigma （l_i*w_i）树叶节点的权值\*从根到节点的长度

每次把最小的两个节点合并起来，父节点的权值是两个节点相加。

##### 最短树：kruskal&prim

kruskal：边权排序，从小到大加，形成回路就跳过这条边

prim：选距离“树”集合最近的一个点加入“树”

破圈法：找到一个圈，把权值最大的边删除



#### Chapter4. 平面图与图的着色

def. 面，域，域的边界，无限域，内部域，域的相邻，可平面图在平面上的一个嵌入称为平面图

**测地变换**--> 可平面<=>可球面

thm. **平面连通图的欧拉公式**：d = m - n + 2

k个连通支， d = m - n + 1 + k

一般平面图， d >= m - n + 2

Thm. 设平面**连通图**G没有割边，每个域的边界数至少是t，则$m\le \frac{t(n-2)}{t-2}$

​	证明过程： t\*d<=2m

def. **极大平面图**：再加边就不能是平面图了（连通，无割边，每个域的边界数都是3，3d=2m）

极大平面图中， m = 3n - 6   ;    d = 2n - 4

简单平面图中，m <= 3n - 6 ;    d <= 2n - 4

thm. 简单平面图G中存在度小于6的节点。--> K7不是平面图

**K5**是节点最少的非平面图（证明：m<=3n-6）

K3,3不是平面图的证明方法！！！没有三角形，4d<=2m

<span style=color:blue> $ K_5 和 K_{3,3}分别记为K^{(1)}和K^{(2)}图 $ </span>

n<5或者m<9的图一定可平面。

G是可平面图的充要条件是G不存在K型子图（在K1K2的边中间加点）

##### 图的平面性检测

连通自环分割点（每个连通支分别检验，去掉自环，有割点从割点处分离）

删度为2去重边 （重复做！）

##### 对偶图

G为平面图，G一定有唯一的对偶图G*，且为连通图（没有孤立的域）

Thm.若G为平面**连通**图，那么(G\*)\*=G

G的一回路各边在对偶图里对应的边是一个割集（把原来里外两个域割开）

G有对偶图的**充要条件**是G是平面图。

​	`只需证K1、K2无对偶图`

五色猜想的证明

##### 色数与色数多项式

色数，边色数

对于非空图G，色数=2当且仅当它没有奇回路

​	`支撑树色数为2，考虑余树边`

色数<=最大度数+1

色数<=1+所有导出子图的最小度数的最大值

色数求法：两个不相邻的点，取把他们连起来和把他们合并为一个点的色数的最小值。



#### Chapter5. 匹配与网络流

def. 匹配，饱和点，非饱和点

匈牙利算法

##### 完全匹配

前提：`二分图`！！

完全匹配，一边配满；完美匹配，两边配满

Thm. **Hall定理**：二分图中，完全匹配的充要条件：对于X的任意子集A，恒有$\Gamma(A)\ge A$

col.若二分图中X里每个点度数>=k, Y里每个点度数<=k,那么一定有X到Y的完全匹配

**最小覆盖**

def. 二分图邻接矩阵里选行、列，每个1都要被覆盖；即每一个边都至少有一断点被选中

最大匹配数r = 最小覆盖数s。

`证明：s>=r好证，r>=s调整顺序，分成四块矩阵，证其中两块有完全匹配，妙！`

##### 最佳匹配（最大权匹配）

此时满足|X|=|Y|

矩阵，每行是每个人，每列是一项工作。

一开始，行的界值$l(x_i)=max(c_{ij})$ 每行的最大值；列的界值是0

然后构造矩阵B，$b_{ij}=l(x_i)+l(y_i)-c_{ij}$

接下来每次：

1、对零元素进行最小覆盖，框出行列 ---> 如果s=n，结束，所有x、y界值相加为ans

2、在**未覆盖**的元素中找到**最小**非零元，圈出来$\delta$

3、修改矩阵：行列双重覆盖元：+$\delta$ ；都没覆盖：-$\delta$

4、修改界值：行没有覆盖：-$\delta$；列覆盖了：+$\delta$



##### 网络流

f_ij 边流量  c_ij 边容量 f 允许流分布    饱和边、非饱和边

最大流 = 最小割

Ford-Fulkerson最大流标号算法：

找S到T的路，标来的点以及正or反向边、可以增流的最大值；然后修改边权

Edmonds-Karp算法：`复杂度:`$ m^2n $

每次沿最短路增流（先标号先检查，检查所有未标号的邻点）

网络中的增流路不超过m(n+2)/2条

`每条边作为向前边能充当瓶颈最多(n+2)/4次，向后边也是`



#### Chapter7. 代数结构预备知识

`thm`. 设f是A到B的映射，$gf=I_A,fh=I_B,则g=h$

​	`proof.` $g=gI_B=g(fh)=(gf)h=I_Ah=h$ 可逆映射的逆映射是唯一的！

自反性、对称性、传递性--> 等价关系、等价类、代表元 （x~a表示x与a等价关系)

def. **等价类族**：所有等价类集合组成的集合，也是A关于~的商集。记为$\vec{A}或者$A/~

def **自然映射**：A到A/~ ，满射



#### <span style=color:blue>代数系统</span>(A,f_1,f_2,...,f_s)

def. 二元运算、n元运算：从$A^n到A$的映射。（重点：封闭性！）

代数系统：非空集合+运算

def. 交换律、结合律、指数律的定义、左右单位元（单位元唯一！）

def. (左/右)可逆元：前提是有`单位元`的代数系统。有结合律时可逆元唯一。

def. 同类型代数系统：f_1...f_s 是几元的运算，几是一样的

def. 代数系统的**同构**：(X,\*)(Y,#) f双射，f(a*b)=f(a)#f(b)

f映射，则为**同态**

 (f(X),#)是(Y,#)的子代数，f(X)是在f作用下X的同态象

单同态，满同态（性质见课本145）；自同态，自同构



#### Chapter8. 群

半群：S非空集合，\*二元运算，\*满足**结合律**，则代数系统(S, *)称为半群。

幺半群：半群中有单位元e存在，(M, *, e)

​		交换幺半群：*满足交换律

​		循环幺半群：M里存在g，使得M里任意一元素可表示为g的次方（g称为生成元）

​		thm. 循环幺群是可交换幺群。

子半群：半群的子集，且在*作用下封闭。

子幺群：幺群的子集，且在*作用下封闭，并且包含**e**



定理8.1.3 把满同态改成同态是否成立？

非空子集H是G子群的充要条件：对任意H里的a，b；都有ab^-1属于H。

H是G子群的充要条件：封闭性，单位元，逆元素



def. 循环群、生成元、循环群的阶

循环群不一定是幺群！例子：(N+, +)



def. 一一变换群：非空集合A的所有一一变换关于变换的乘法所形成的群，E(A)

def. 变换群：E(A)的子群叫做变换群

def. 置换群：当A是有限集合时，一个一一变换就叫做“n元置换”，形成的群是置换群

def.对称群：n！个置换构成的群

def.交错群：1/2*n！个偶置换构成的群

cayley定理：任何群G与一个变换群同构！

-----> 任意一个有限群G，都与一个置换群同构



H是G的一子**群**，则H在G中的一个左陪集： $aH=\{ah|h\in H\}$

陪集的7个性质

群G关于其子群H的左陪集的个数，称为H在G中的指数 [G:H]

Lagrange定理的3个推论（第三个可以再看一遍！）



def. 正规子群： H是G的一个子群，使得任意G中的a，都有aH=Ha

与群同构的代数系统是群

群的同态象是群
