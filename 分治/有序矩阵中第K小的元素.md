## [有序矩阵中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)

给定一个 *`n x n`* 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第 `k` 小的元素。
请注意，它是排序后的第 `k` 小元素，而不是第 `k` 个不同的元素。

**示例：**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
   ],
k = 8,

返回 13。
```

**提示：**
你可以假设 k 的值永远是有效的，`1 ≤ k ≤ n2 `。





暴力法比较直观，虽然没什么意义...

```java
public int kthSmallest(int[][] matrix, int k) {
        int len = matrix[0].length;
        int count = 0;
        int[] temp = new int[len*matrix.length];
        for (int i=0;i<matrix.length ;i++) {
            for (int j = 0; j < len; j++) {
                temp[count++] = matrix[i][j];
            }
        }
        Arrays.sort(temp);
        return temp[k+1];
    }

```



最大堆

```java
  public int kthSmallest(int[][] matrix, int k) {
      //o2-o1为优先最大值，o1-o2为优先最小值
         Queue<Integer> queue = new PriorityQueue<>(((o1, o2) -> o2-o1));
        for(int i=0;i<matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                if(queue.size()<k) queue.offer(matrix[i][j]);
                else if(queue.peek()>matrix[i][j]){
                    queue.poll();
                    queue.offer(matrix[i][j]);
                }
            }
        }
        return queue.poll();
    }
```

