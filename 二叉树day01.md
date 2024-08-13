#  二叉树

## 二叉树的理论基础


###  二叉树的种类

1.  满二叉树

![满二叉树](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806185805576.png)

满二叉树的特点如上图所示，具有叶子最多的特点，其结点公式为2^k-1，其中k为深度

1.  完全二叉树

![完全二叉树](https://code-thinking-1253855093.file.myqcloud.com/pics/20200920221638903.png)

完全二叉树具有除最底层节点不是全满外，其余每层节点数都达到最大值，并且下面一层的节点从左到右必须是连续的，一旦有空隔就不是完全二叉树，其中节点个数为1~2^k-1 ,其中k为深度

3.  二叉搜索树

前面介绍的树，都没有数值的，而二叉搜索树是有数值的了，二叉搜索树是一个有序树。

- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
- 它的左、右子树也分别为二叉排序树

![完全二叉树](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806190304693.png)

4.  平衡二叉搜索树

平衡二叉搜索树：又被称为AVL（Adelson-Velsky and Landis）树，且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

![平衡二叉搜索树](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806190511967.png)

<br />

### 二叉树的存储方式
---

1. 链式存储

   下面提供二叉树的C++链式存储代码
```  C++
#include<iostream>
#include<queue>

using namespace std;

struct TreeNode{
    int value;
    TreeNode *left;
    TreeNode *right;

    TreeNode(int x)；value(x),left(nullptr),right(nullptr);
};

TreeNode *createTree(TreeNode *head){
    if(head==nullptr)
    return nullptr;
    TreeNode *root=head;

    queue<TreeNode *>q;
    q.push(root);

    while(head!=nullptr){
        TreeNode *parent=q.front();
        q.pop();
        if(head->left!=nullptr){
            parent->left=head->left;
            q.push(parent->left);
        }
        head=head->right;
        if(head!=nullptr){
            parent->right=head;
            q.push(parent->right);
            head=head->right;
        }
    }
    return root;
}
```
2. 数组存储

   等我学完再来补吧hhhh
### 二叉树的遍历方式
---
1. 深度优先遍历（也即深度优先搜索）：先往深走，遇到叶节点在返回（常用递归实现）
2. 广度优先遍历：一层一层的去遍历（常用队列实现）

从深度优先遍历和广度优先遍历进行扩展，才有如下方式
---
深度优先遍历[均可用递归法，迭代法实现]
- 前序遍历(中左右)
- 中序遍历(左中右)
- 后序遍历(左右中)
  
  下面给一副图，大家理解一下
![遍历图](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806191109896.png)
广度优先遍历[迭代法实现]
- 层序遍历

---
下面给出前中后序的C++代码

- 前序：
``` C++
void traversal(TreeNode *cur,vector<int> &vec){
    if(cur==nullptr)
    return ;
    vec.push_back(cur->value);
    traversal(cur->left,vec);
    traversal(cur->right,vec);
}
```
- 中序:
``` C++
void traversal(TreeNode *cur,vector<int> &vec){
    if(cur==nullptr)
    return ;
    traversal(cur->left,vec);
    vec.push_back(cur->value);
    traversal(cur->right,vec);
}
```
- 后序:
``` C++
void traversal(TreeNode *cur,vector<int> &vec){
    if(cur==nullptr)
    return;
    traversal(cur->left,vec);
    traversal(cur->right,vec);
    vec.push_back(cur->value);
}
```
---
最后调用这些函数即可，调用函数如下：
``` C++
vector<int>Traversal(TreeNode *root){
    vector<int>result;
    traversal(root,result);
    return result;
}
```
---
以上就是今天的内容，Thanks for your watching.