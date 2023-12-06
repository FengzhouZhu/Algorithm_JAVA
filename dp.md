## 动态规划

### Example
给定一个三角形 triangle ，找出自顶向下的最小路径和。
每一步只能移动到下一行中相邻的结点上。相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。也就是说，如果正位于当前行的下标 i ，那么下一步可以移动到下一行的下标 i 或 i + 1 。

用f[i][j]表示从三角形顶部走到位置(i,j)的最小路径和。这里的位置(i,j)指的是三角形中第i行第j列（均从0开始编号）的位置。

由于每一步只能移动到下一行「相邻的节点」上，因此要想走到位置(i,j)，上一步就只能在位置(i−1,j−1) 或者位置(i−1,j)。我们在这两个位置中选择一个路径和较小的来进行转移，状态转移方程为：

f[i][j]=min (f[i-1][j-1], f[i-1][j])+c[i][j]

注意第i行有i+1个元素，它们对应的j的范围为[0,i]。当j=或j=i时，上述状态转移方程中有一些项是没有意义的。例如当j=0时，f[i−1][j−1] 没有意义，因此状态转移方程为：

f[i][0]=f[i−1][0]+c[i][0]

即当我们在第i行的最左侧时，我们只能从第i−1行的最左侧移动过来。当j=i 时，f[i−1][j] 没有意义，因此状态转移方程为：
f[i][i]=f[i−1][i−1]+c[i][i]

最终的答案即为f[n−1][0]到f[n−1][n−1]中的最小值，其中n是三角形的行数。

```
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int[][] f = new int[n][n];
        f[0][0] = triangle.get(0).get(0);
        for(int i = 1;i < n;++i){
            f[i][0] = f[i-1][0] + triangle.get(i).get(0);
            for(int j = 1;j < i;++j){
                f[i][j] = Math.min(f[i-1][j-1],f[i-1][j])+triangle.get(i).get(j);
            }
            f[i][i] = f[i-1][i-1] + triangle.get(i).get(i);
        }
        int minTotal = f[n-1][0];
        for(int i = 1;i < n;++i){
            minTotal = Math.min(minTotal,f[n-1][i]);
        }
        return minTotal;
    }
}
```

### 使用场景
满足两个条件

1满足以下条件之一
求最大/最小值（Maximum/Minimum ）
求是否可行（Yes/No ）
求可行个数（Count(*) ）
2满足不能排序或者交换（Can not sort / swap ）

**位置可交换example**
```
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> num_set = new HashSet<Integer>();
        for(int num:nums){
            num_set.add(num);
        }
        int longestStreak = 0;
        for(int num:num_set){
            if(!num_set.contains(num-1)){
                int currentNum = num;
                int currentStreak = 1;
                while(num_set.contains(currentNum+1)){
                    currentNum += 1;
                    currentStreak += 1;
                }
                longestStreak = Math.max(longestStreak,currentStreak);
            }
        }
        return longestStreak;
    }
}
```
### 四点要素
状态 State
灵感，创造力，存储小规模问题的结果
方程 Function
状态之间的联系，怎么通过小的状态，来算大的状态
初始化 Intialization
最极限的小状态是什么, 起点
答案 Answer
最大的那个状态是什么，终点

### 题型（矩阵类型）
给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。
说明：每次只能向下或者向右移动一步。
