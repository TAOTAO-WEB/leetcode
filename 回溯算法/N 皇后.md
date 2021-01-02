## [N 皇后](https://leetcode-cn.com/problems/n-queens/)

*n* 皇后问题研究的是如何将 *n* 个皇后放置在 *n*×*n* 的棋盘上，并且使皇后彼此之间不能相互攻击。

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

**示例：**

```
输入：4
输出：[
 [".Q..",  // 解法 1
  "...Q",
    "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```

**提示：**

- 皇后彼此不能相互攻击，也就是说：任何两个皇后都不能处于同一条横行、纵行或斜线上。



```java
 public List<List<String>> solveNQueens(int n) {
        List<List<String>> rs = new ArrayList<>();
        int[] queens = new int[n];
        Set<Integer> col = new HashSet<>();
        Set<Integer> dia1 = new HashSet<>();
        Set<Integer> dia2 = new HashSet<>();
        backtrack(rs,queens,n,0,col,dia1,dia2);
        return rs;
    }

    private void backtrack(List<List<String>> rs,int[] queens,int n,int row,Set<Integer> col,Set<Integer> dia1,Set<Integer> dia2){
        if(row==n){
            List<String> board = generateBoard(queens,n);
            rs.add(board);
        }
        else {
            for(int i = 0;i<n;i++){
                if(col.contains(i)) continue;
                int diagonal1 = row-i;
                if(dia1.contains(diagonal1)) continue;
                int diagonal2 = row+i;
                if(dia2.contains(diagonal2)) continue;
                queens[row] = i;
                col.add(i);
                dia1.add(diagonal1);
                dia2.add(diagonal2);
                backtrack(rs,queens,n,row+1,col,dia1,dia2);
                queens[row] = -1;
                col.remove(i);
                dia1.remove(diagonal1);
                dia2.remove(diagonal2);
            }
        }
    }

    private List<String> generateBoard(int[] queens,int n){
        List<String> board = new ArrayList<>();
        for(int i = 0;i<n;i++){
            char[] row = new char[n];
            Arrays.fill(row,'.');
            row[queens[i]] = 'Q';
            board.add(new String(row));
        }
        return board;
    }
```

