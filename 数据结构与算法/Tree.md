# 树专题

### **平均复杂度**：O(logN)

**数学定义**：N个节点和N-1条边。（只有一个根节点没有指向父节点的边）

### **概念**：

结构上：根、边、树叶
关系上：父亲、儿子、兄弟、祖父、孙子，祖先，后裔，真祖先，真后裔
几何上(纵向)：路径(父-子)、长。深度(向下，根为0)，高度(向上，叶为0)。

```java
// 常规树节点声明
class TreeNode{
     Object element;
		TreeNode firstChild;
		TreeNode nextSibling;             
}
```

**实现**：TreeSet、TreeMap

### **应用**：

文件系统
搜索操作
算术表达运算
二叉树在编译器的设计中应用：表达式树读取（中序、前序、后序遍历），构建（栈）

### **形式：**

数组形式的树
Map形式的树
类结构的树
普通树：(孩子数目不确定)链表实现 { 自己的值，firstChild，nextSibling}

### 遍历：就是函数嵌套自身，

深度遍历：当能继续时，先遍历孩子
广度遍历：当能继续时，先遍历兄弟

因此，树的操作的思考单元(执行单元)，是在最小父子之间。

#### **前(先)序遍历**

> **前(先)序遍历** PreOrder traversal：对节点的处理工作在它的诸儿子被访问之前。运行时间O(N)

```java
// 分级列出文件系统中目录
private void listAll( int depth ){
		printName( depth ); // 打印当前深度目录
		if( isDirectory() ){ // 如果当前还是目录，可以继续深入
    		for(file : directory){
    			file.listAll( depth + 1);
        }
    }               
}
// 递归的驱动函数, 深度控制缩进
public void listAll(){
	listAll(0);
}
```

#### 后续遍历

> **后续遍历** postorder traversal : 节点的处理工作在诸儿子节点被访问之后。

如： 计算linux中文件占用的磁盘区块大小。

```java
public int size(){
	int totalSize = sizeOfThisFile(); // 当前非文件夹文件总大小
	if( isDirectory() ){
		for(file in directiory){
			totalSize += file.size();
    }
  }
	return totalSize();
}
```

#### 中序遍历

> 中序遍历: 在二叉树中中序遍历才有意义

#### 层序遍历

需要用到深度信息。[102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

### 二叉树 (B树)

```java
// 节点类,类似双链表
class BinaryNode{
	Object element;
	BinaryNode left;
	BinaryNode right;                 
}
```

特性：

1. 平衡二叉树深度远小于节点个数 (depth << N), 平均深度 O(根号N)
2. 在编译器设计领域，用来表示表达式的树

树一般采用递归形式解决，由于二叉查找树凭据深度logN，因此不用担心栈空间被耗尽。

#### 二叉查找树(BST)

```java


public class BinarySearchTree<AnyType extends Comparable<? super AnyType>>{
	// BinaryNode类,静态内部类
	private static class BinaryNode<AnyType>{
		BinaryNode(AnyType theElement){
			this(theElement, null, null);
  	}
		BinaryNode(AnyType theElement, BinaryNode<AnyType> lt, BinaryNode<AnyType> rt){
			element = theElement; left = lt; right =rt;
  	}
		AnyType element;
		BinaryNode<AnyType> left;
		BinaryNode<AnyType> right;                   
	}
	// 根
	private BinaryNode<AnyType> root;
	// 构造函数
	public BinarySearchTree(){ root = null; }
	// 使空/判空
	public void makeEmpty(){ root = null; }
	public void isEmpty(){ return root == null;}
  // 包含/查找
	public boolean contains(AnyType x){ return contains(x, root); }  // 驱动模式
	public AnyType findMin(){ 
		if( isEmpty() ) throw UnderflowException(); 
		return findMin(root).element;
  }  
	public AnyType findMax(){
		if( isEmpty() ) throw UnderflowException();
		return findMax(root).element;
  }
	// 插入、删除、打印
	public void insert( AnyType x ){ root = insert(x, root); }
	public void remove( AnyType x ){ root = remove(x, root); }
	public void printTree(){}

	// 一旦出现比较，就要考虑“不重不漏”原则。
	private boolean contains( AnyType x, BinaryNode<AnyType> t ){
		if( t == null ){ return false; }
		int compareResult = x.compareTo( t.element ); // 比较当前节点
		if( compareResult < 0 ) return contains( x, t.left ) // 小于根，查找左边
		else if( compareResult > 0 ) return contains( x, t.right ) // 大于根，查找右边
		else return true; // 等于根，返回。
	}
	private BinaryNode<AnyType> findMin( BinaryNode<AnyType> t ){}
	private BinaryNode<AnyType> findMax( BinaryNode<AnyType> t ){}
	private BinaryNode<AnyType> insert( AnyType x, BinaryNode<AnyType> t ){}
	private BinaryNode<AnyType> remove( AnyType x, BinaryNode<AnyType> t ){}
	private void printTree( BinaryNode<AnyType> t ){}
                  
}
```



特点：

1. **深度受控**：深度平均值O(log N) （小于根号N）, 最坏深度O(N-1),退化到链表。 
2. **顺序受控**：左边节点小于根，右边节点大于根。中序遍历是升序序列
3. **可比较性**：任意两项可使用compareTo方法进行比较



### B+树

### 红黑树

### 并查集 Disjoints

树的连通性，集合性。

### 二项树

### 前缀树

### 后缀树

 



 

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

  ```java
Class BSTIterator {
    private TreeNode root;
    private int min;
		public BSTIterator(TreeNode root){
				this.root = root;
				TreeNode temp = root;
				while(temp != null){
					min = temp.val;
					temp = temp.left;
        }
    }
    
		// 假设树中元素大小互异
		public int next(){
			int result = min;
			TreeNode temp = root;
			while(temp != null){
				if(temp.val > min){
					min = temp.val;
					temp = temp.left;
        	}else if(temp.val == min){
        		temp = temp.right;
        	}
      }
      if(min == result){
      	min == null;
      }
      return result;
		}
    
		public boolean hasnext(){
			if( min != null ){
				return true;
      }
      return false;
		}            
}
  ```

