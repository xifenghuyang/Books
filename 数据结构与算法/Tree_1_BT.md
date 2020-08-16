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

	/** 一旦出现比较，就要考虑“不重不漏”原则。
		最后的两个递归属于尾递归，可以用while替换。栈空间O(log N)
		或者可以使用一个函数对象，而不一定要要求树中的项是Comparable的。
	*/
	private boolean contains( AnyType x, BinaryNode<AnyType> t ){
		if( t == null ){ return false; }
		int compareResult = x.compareTo( t.element ); // 比较当前节点
		if( compareResult < 0 ) return contains( x, t.left ) // 小于根，查找左边
		else if( compareResult > 0 ) return contains( x, t.right ) // 大于根，查找右边
		else return true; // 等于根，返回。
	}
	// 找最小：递归形式
	private BinaryNode<AnyType> findMin( BinaryNode<AnyType> t ){
		if( t == null ) return null;
		else if( t.left == null ) return t; // 没有子节点，就返回自身
		return findMin( t.left );
  }
	// 找最大：循环形式。对t的改变时安全的，因为是使用 引用的拷贝
	private BinaryNode<AnyType> findMax( BinaryNode<AnyType> t ){
		if( t == null ) return null;
		while( t.right != null ) t = t.right;
		return t;
  }
	/** 插入：就是在查找为null的位置新建
		可以像contains函数沿着树查找。重复节点不执行插入；
		重复元素，也可以在节点的记录中使用一个附加域，表示发生次数。
		t引用了根，而根又在第一次插入时发生变化，因此返回对新书根的引用。
	*/
	private BinaryNode<AnyType> insert( AnyType x, BinaryNode<AnyType> t ){
		if( t == null ){ return new BinaryNode<>( x, null, null ); }
		int compareResult = x.compareTo(t.element);
		if( compareResult < 0 ) t.left = insert(x, t.left); // 将插入后的左子树返回
		else if( compareResult > 0 ) t.right = insert(x, t.right); // 将插入后的右子树返回
		else ; // 重复元素
		return t;
	}
	/**
	先查找，再删除
	1. 节点是一片叶子，直接删除
	2. 节点只有1个儿子，儿子取代父节点地位。
	3. 节点有2个儿子，右子树的最小节点代替该点，再删除右子树中的最小点。变相先下移再删除。
	*/
	private BinaryNode<AnyType> remove( AnyType x, BinaryNode<AnyType> t ){
		if( t==null ) return t;
		int compareResult = x.compare(t.element);
		if(compareResult < 0) t.left = remove(t.left);
		else if(compareResult > 0) t.right = remove(t.right);
		// 找到节点
		else if( t.left != null && t.right != null ) { // 有2个孩子
			t.element = findMin(t.right).element; // 效率提升点
			t.right = remove(t.element, t.right);
    }else{ // 有一个孩子，或无孩子
    	t = t.left != null ? t.left : t.right; 
    }
    return t;
	}
	private void printTree( BinaryNode<AnyType> t ){}
                  
}
```

特点：

1. **深度受控**：深度平均值O(log N) （小于根号N）, 最坏深度O(N-1),退化到链表。 
2. **顺序受控**：左边节点小于根，右边节点大于根。中序遍历是升序序列
3. **可比较性**：任意两项可使用compareTo方法进行比较

双孩子情况下，删除操作的效率提升问题：

因为进行了2趟搜索，查找右子树中最小值+删除右子树中最小节点。可以重写removeMin方法，在查找右子树最小节点的同时，删除该节点。

> **懒删除lazy deletion**

用标记替代真正删除，当删除次数不多是可以采用这种策略。要删除的元素仍留在树中，只是被标记为删除。好处;

1. 如果有重复项时，可以采用次数减一。
2. 被删除的项重新插入，可以避免分配一个新单元的开销。

**界**：任意节点平均深度O(logN)，所有操作的平均时间logN，N个节点的操作O(N logN), 500个节点预期深度9.98

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

