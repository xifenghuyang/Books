# 树专题

**平均复杂度**：O(logN)

**数学定义**：N个节点和N-1条边。（只有一个根节点没有指向父节点的边）

**概念**：

结构上：根、边、树叶

关系上：父亲、儿子、兄弟、祖父、孙子，祖先，后裔，真祖先，真后裔

几何上(纵向)：路径(父-子)、长。深度(向下，根为0)，高度(向上，叶为0)。

**实现**：TreeSet、TreeMap

**应用**：

文件系统

搜索操作

算术表达运算

二叉树在编译器的设计中应用：表达式树读取（中序、前序、后序遍历），构建（栈）

**形式：**

数组形式的树

Map形式的树

类结构的树

普通树：(孩子数目不确定)链表实现 { 自己的值，firstChild，nextSibling}

遍历：就是函数嵌套自身，

深度遍历：当能继续时，先遍历孩子

广度遍历：当能继续时，先遍历兄弟

因此，树的操作的思考单元(执行单元)，是在最小父子之间。

 

广搜

深搜

 

层序遍历：需要用到深度信息。[102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

前(先)序遍历 preorder traversal：对节点的处理工作在它的诸儿子之前。

中序遍历

后续遍历 postorder traversal


**二叉树****(B****树****) binary tree**：平均深度O( )![img](data:image/png;base64,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)

**二叉查找树****BST**：平均深度O(logN) 左边节点小于根，右边节点大于根。有序的树。

树中的两项总是可以使用compareTo方法进行比较

B+树

红黑树

###  并查集 Disjoints

这种数据结构使用**一个简单的数组**，实现每种操作的**常数平均时间**，分析却比较困难。
是对等价关系的一种表达：自反性 aRa; 对称性 aRb bRa；传递性 aRb bRc -> aRc.
电气连通性，城市间关系，道路关系。

#### 动态等价性问题

**初始状态**：N个单元素不想交集合。disjoint
只允许**2种操作**：**find** (查) 和 **union** (并) 添加关系
**dynamic**: on-line / off-line,

情景问题**数字化**：假设所有元素均已从0 ~ N-1进行编号，且编号方法，可以用某个hash方法得到。
**开始**: 集合Si = { i }, i = 0 ~ N-1
**关键**：find(a) == find(b) 为true时，a和b在同一个集合
**时空分析**：find和union不能同时以常数最坏情形运行时间执行。

**提速find**： 1）使用数组保存每个元素的find值。find ~ O(1) ; 2) 使用链表保存元素。更新等价集合可能O(N^2)
**提速union(控制深度)**：跟踪每个等价集合的大小，并在执行union时，将较小的等价集合的名字改成较大等价集合名字。O(N log N), 任意 M 次find和直到 N-1 union 最多花费 O (M+N log N)时间。

**find的本质**：当两个元素属于相同集合时，执行find返回相同的名字。
**实现**：用树来表示每个集合，输入时树的集合 森林。存储在数组中的树结构。find(x)操作与x节点的深度成正比。

 

前缀树

后缀树

 

树一般采用递归形式解决，由于二叉查找树凭据深度logN，因此不用担心栈空间被耗尽。

 

**经典练习**

按层次打印文件：前序遍历

计算文件和：后序遍历

Leetcode 114：树转链表。后序遍历中，先左后右和先右后左的区别。（复杂问题，采用思路分解方式）

 

链表

单链表

双链表

##### 练习：

1. https://leetcode-cn.com/problems/redundant-connection-ii/submissions/

```java
class Solution {
                     
  // 关键词：并查集                 
  public int[] findRedundantDirectedConnection(int[][] edges){
  	int n = edges.length;
  	int[] father = new int[n+1]; // 初始化列表，1-N
  	int[] inDegree = new int[n+1]; // 1~N，默认值为0
  	// 初始化father数组，自根
  	for(int i=0; i<=n; i++){
  		father[i] = i;
    }
  	// 找入度为2的节点
  	int twoDegreePoint = -1;
  	for(int[] points : edges){
  		inDegree[points[1]]++;
  		if(inDegree[points[1]]==2){
  			twoDegreePoint = points[1];
      }
    }
    // 存在入度为2的节点，必然删去其中一条边
  	if(twoDegreePoint != -1){
  		for(int[] points : edges){
  			int xRoot = findRoot(points[0]);
  			int yRoot = findRoot(points[1]);
  			if(xRoot != yRoot){
  				father[yRoot] = xRoot; // 后树挂前树
        }else{
        	return points; // 找到多出来的边，结束
        }
      }
    }
    // 入度为1情况。
    
    
    
  }
  
  // 并查集，找根
  private int findRoot(int x, int[] father){
  	int xRoot = x;
  	// 不是自根节点，就一直往上找
  	while(father[xRoot] != xRoot){
  		father[xRoot] = father[father[xRoot]]; // 路径压缩
  		xRoot = father[i];
    }
    return xRoot;
  }
}
```

