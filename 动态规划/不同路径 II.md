## [ 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。



> 还是先尝试bfs，大的测试用例超出时限...

```java
 public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        return count(obstacleGrid,0,0);
    }

    private int count(int[][] grid,int x,int y){
        if(x>grid.length-1 || y>grid[0].length-1 || grid[x][y]==1) return 0;
        if(x==grid.length-1 && y==grid[0].length-1) return 1;
        return count(grid,x+1,y) + count(grid,x,y+1);
    }
```

> dp

```java
 public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] rs = new int[m][n];
        if(obstacleGrid[0][0]==0) rs[0][0]=1;
        else rs[0][0]=0;
        
        for(int i=1;i<m;i++){
            if(obstacleGrid[i][0] == 0 && rs[i-1][0]!=0) rs[i][0] = 1;
            else rs[i][0] = 0;
        }
        for(int i=1;i<n;i++){
            if(obstacleGrid[0][i] == 0 && rs[0][i-1]!=0) rs[0][i] = 1;
            else rs[0][i] = 0;
        }
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j]==1) rs[i][j]=0;
                else rs[i][j] = rs[i-1][j]+rs[i][j-1];
            }
        }
        return rs[m-1][n-1];
    }
```

