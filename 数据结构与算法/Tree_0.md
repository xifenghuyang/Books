# 树专题

### **平均复杂度**：O(logN)

**数学定义**：N个节点和N-1条边。（只有一个根节点没有指向父节点的边）

### **概念**：

- 结构上：根、边、树叶
- 关系上：父亲、儿子、兄弟、祖父、孙子，祖先，后裔，真祖先，真后裔
- 几何上(纵向)：路径(父-子)、长。深度(向下，根为0)，高度(向上，叶为0)。

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

1. 文件系统
2. 搜索操作
3. 算术表达运算
4. 二叉树在编译器的设计中应用：表达式树读取（中序、前序、后序遍历），构建（栈）

### **形式：**

1. 数组形式的树
2. Map形式的树
3. 类结构的树
4. 普通树：(孩子数目不确定)链表实现 { 自己的值，firstChild，nextSibling }

### 遍历：就是函数嵌套自身，

- 深度遍历：当能继续时，先遍历孩子
- 广度遍历：当能继续时，先遍历兄弟

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
