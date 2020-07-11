## [路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)


给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

dfs

```java
public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> rs = new ArrayList<>();
        if(root==null) return rs;
        List<Integer> list = new ArrayList<>();
        temp(root,sum,list,rs,0);
        return rs;
    }

private void temp(TreeNode root,int sum,List<Integer> list,List<List<Integer>> rs,int t){
        if(root.left==null && root.right==null){
            if(t+root.val==sum) {
                list.add(root.val);
                rs.add(new ArrayList<>(list));
            }
        }
        else if(root.left!=null && root.right!=null){
            list.add(root.val);
            temp(root.left,sum,new ArrayList<>(list),rs,t+root.val);
            temp(root.right,sum,new ArrayList<>(list),rs,t+root.val);
        }
        else if(root.left!=null){
            list.add(root.val);
            temp(root.left,sum,new ArrayList<>(list),rs,t+root.val);
        }
        else {
            list.add(root.val);
            temp(root.right,sum,new ArrayList<>(list),rs,t+root.val);
        }
    }
```

