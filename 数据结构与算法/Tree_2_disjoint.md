###  2.  并查集 Disjoints

这种数据结构使用**一个简单的数组**，实现每种操作的**常数平均时间**，分析却比较困难。
是对等价关系的一种表达：自反性 aRa; 对称性 aRb bRa；传递性 aRb bRc -> aRc.
电气连通性，城市间关系，道路关系。

#### 2.1 动态等价性问题

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
**实现**：用树来表示每个集合，输入时树的集合 森林。存储在数组中的树结构。find(x)操作代价与x节点的深度成正比。

#### 2.2 不相交集合基础架构

 ```java
// 不相交集合架构
public class DisjSets{
  private int[] s;
                    
  // 初始化，0~N-1的N个元素, -1 代表自根元素/自集合
	public DisJsets( int numElements){
		s = new int[numElements];
		for( int i = 0; i < s.length; i++ ){ s[i] = -1; }
  }
                    
  // 并，将一棵树并到另一颗树上，数组操作
  public void union(int root1, int root2){
  	s[root2] = root1; // 默认将树2由自根改为指向树1.
  }   
                    
  // 查，find的等价性, 查一个元素所处的集合 = 所在树的根 = 数组中-1的元素
  public void find(int x){
  	if(s[x] < 0){
  		return x;
    }
    return find(s[x]);
    // 尾递归可用while表达
  	// while(s[x] >= 0){
  	//		x = s[x];
  	// }
  	// return x;
  }                    
}
 ```

#### 2.3 改进union提升效率

union合并的选择具有随意性，打破随意性，合并时，让小树成为大树的子树。

> **按大小求并 union by size**

**已证明的界**：如果所有union操作，都是按大小进行，则合并后任何节点深度均不超过**logN**
进而，深度最多到**logN** ，find操作又与深度成正比，因此一次find的花费 logN.

**记录树的大小**：数组中每个表示根的负数(-1)，改为记录树大小的负值。(即用了正负标记根和，又用了值标记大小)

> 按高度求并 union by height

**界**：同样保证了所有树的深度最多是**logN**
让低树成为高树的子树。按高度求并是按大小求并的简化。根处存的是高度减1，因为初始值为-1，而初始高为0。

```

```
