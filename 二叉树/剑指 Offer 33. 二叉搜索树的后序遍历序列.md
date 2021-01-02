## [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

**示例 1：**

```
输入: [1,6,3,2,5]
输出: false
```

**示例 2：**

```
输入: [1,3,2,6,5]
输出: true
```

二叉搜索树，左子树比根节点小，右子树比根节点大

后续遍历为left->right->root,可以发现规律，最后一个数值一定是根节点，从左到右找到找到第一个比最后一个值大的数，就是根节点的右节点，之后判断右节点后面的数是否都比根节点大，如果不是则不是二叉搜索树。

```java
public boolean verifyPostorder(int[] postorder){
        return helper(postorder,0,postorder.length-1);
    }

    boolean helper(int[] postorder,int left,int right){
        if(left>=right) return true;
        int root = postorder[right];
        int mid = left;
        while (postorder[mid]<root){
            mid++;
        }
        int temp = mid;
        while (temp<right){
            if(postorder[temp++]<root){
                return false;
            }
        }
        return helper(postorder,left,mid-1) && helper(postorder,mid,right-1);
    }
```

