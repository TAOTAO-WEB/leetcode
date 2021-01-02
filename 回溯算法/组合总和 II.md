## [组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
    [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
    [5]
]
```

这题的关键在于如何去重，自己写的方法效率比较低，先数组排序，回溯算法之后用set去重，set接近hashmap底层效率较低。

```java
List<List<Integer>> rs = new ArrayList<>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<Integer> temp = new ArrayList<>();
        Arrays.sort(candidates);
        back(candidates,target,0,0,temp);
        Set<List<Integer>> set = new HashSet<>(rs);
        rs = new ArrayList<>(set);
        return rs;
    }

    private void back(int[] candidates,int target,int cur,int index,List<Integer> temp){
        if(cur==target) {
            rs.add(new ArrayList<>(temp));
            return;
        }
        if(cur>target || index>candidates.length-1) return;
        temp.add(candidates[index]);
        back(candidates,target,cur+candidates[index],index+1,temp);
        temp.remove(temp.size()-1);
        back(candidates,target,cur,index+1,temp);
    }
```

