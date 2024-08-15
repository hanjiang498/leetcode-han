### 代码随想录算法训练营第2天| 
## 209. Minimum Size Subarray Sum

time complexity: O(n)
Space: O(1)

思路: 双指针滑动窗口

在右指针触底之前，累加当前右指针值，如果超过了target，则尝试从左指针的值开始减，看能最多减多少个左边的值，每次有达成target的window，记录最小长度。
    

Java:
```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left = 0, right =0;
        int minLength = Integer.MAX_VALUE;
        int currentSum =0;
        while(right< nums.length){
            currentSum += nums[right++];
            while(currentSum>=target){
                minLength = Math.min(minLength, right-left);
                currentSum -= nums[left++];
            }
        }
        return minLength == Integer.MAX_VALUE? 0:minLength;
    }
}
```
Python3:
```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        right = 0
        min_length = maxsize
        window_accumulate = 0
        while right < len(nums):
            window_accumulate += nums[right]
            right += 1
            while window_accumulate >= target:
                min_length = min(min_length, right - left)
                window_accumulate -= nums[left]
                left += 1
        return 0 if min_length == maxsize else min_length
```


## 59. Spiral Matrix II。

time complexity: O(M), M = n * n, number of elements
Space: O(M),
状态： 隔了蛮久做这道题，忘记以前的做法了，之后对边了下，觉得还是之前的写法更简洁

思路: 确立起始位置，左边界，右边界，上下边界，在左右边界或者上下边界都相等之前，持续按照 右 下 左 上 的顺序添加数字。
每行列遍历完，对应边界加一或者减一:
  1. 向右遍历，终止条件为碰到右边界，结束后回跳一格并向下移到下一次遍历初始位置，上边界随之+1
  2. 向下遍历，终止条件为碰到下边界，结束后回跳一格并向左移到下一次遍历初始位置，右边界随之-1
  3. 向左遍历，终止条件为碰到左边界，结束后回跳一格并向上移到下一次遍历初始位置，下边界随之-1
  4. 向上遍历，终止条件为碰到上边界，结束后回跳一格并向右移到下一次遍历初始位置，左边界随之+1

Java:
```
class Solution {
    public int[][] generateMatrix(int n) {
        int upperBoarder = 0, leftBoarder = 0;
        int bottomBoarder = n, rightBoarder = n;

        int i=0, j=0;
        int[][] matrix = new int[n][n];
        int num=1;
        while(upperBoarder<bottomBoarder || leftBoarder<rightBoarder) {
            
            //right
            while(j<rightBoarder){
                matrix[i][j++] = num++; 
            }
            i++;
            j--;
            upperBoarder++;
            //down
            while(i<bottomBoarder){
                matrix[i++][j] = num++; 
            }
            i--;
            j--;
            rightBoarder--;
            //left
            while(j>=leftBoarder){
                matrix[i][j--] = num++; 
            }
            i--;
            j++;
            bottomBoarder--;
            //up
            while(i>=upperBoarder){
                matrix[i--][j] = num++; 
            }
            i++;
            j++;
            leftBoarder++;
        }
        return matrix;
    }
}
```
Java previous submitted version, more clear:
```
class Solution {
    public int[][] generateMatrix(int n) {
        List<Integer> result = new ArrayList<>();
        int[][] directions = new int[][]{{0,1}, {1,0}, {0,-1}, {-1,0}};
        int directionIndex = 0;
        //if there is no more to explore, changeDirection will keep increase and will not be reset
        int changeDirection = 0;
        int[][] matrix = new int[n][n];
        matrix[0][0] = 1;

        int i=0,j=0;
        int k=2;
        while(changeDirection <= 1){
        while(i+directions[directionIndex][0]<n && i+directions[directionIndex][0]>=0 &&
              j+directions[directionIndex][1]<n && j+directions[directionIndex][1]>=0 
              && matrix[i+directions[directionIndex][0]][j+directions[directionIndex][1]] == 0){
                changeDirection = 0;
                i=i+directions[directionIndex][0];
                j=j+directions[directionIndex][1];
                matrix[i][j] = k++;
              }
        directionIndex = (directionIndex+1)%4;
        changeDirection++;
        }
        return matrix;
    }
}
```

总结：

59 题，
 1. 终止条件是左边界>右边界，并且上边界>下边界， 而不是≥
 2. 每次遍历完一个方向记得回跳并就位于下一个起始位置，循环比较复杂，容易出错，想清楚再写
