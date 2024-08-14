### 代码随想录算法训练营第一天| 
## 704. 二分查找
文章讲解: [代码随想录](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)

视频讲解: [b站](https://www.bilibili.com/video/BV1fA4y1o715)

状态： 14 分钟 AC, java + python， java 用的 recursion 迭代， python 用的while loop, 花的时间比较久，应该直接用while，会更简单，写java时候在recursion的终止条件上debug了一下

思路: 二分法，

习惯左闭右开，找mid， mid初始为 (left +（length-1)) /2, 比较mid和target, 三种可能：
    
    1. 相等， 找到了目标值，返回index， 此时为mid
    2. target < nums[mid], 则目标值可能在mid左侧，重置right 为mid-1，再找
    3. target > nums[mid], 则目标值可能在mid右侧，重置left 为mid+1，再找

终止条件： left < right， 在递归中，如果进入这一步，则返回-1； 在循环里，如果未找到目标值并返回，则最终返回-1.

Java:
```
class Solution {
    public int search(int[] nums, int target) {
        return bisect(0, nums.length-1, nums, target);
    }

    private int bisect(int start, int end, int[] nums, int target){
        if(start > end) return -1;
        int mid = (start + end)/2;
        if(target==nums[mid]) return mid;
        else if(target < nums[mid]) return bisect(start, mid-1, nums, target);
        else return bisect(mid+1, end, nums, target);
    }

}
```
Python3:
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        return -1
```


## 27. 移除元素。
文章讲解: [代码随想录](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)

视频讲解: [b站](https://www.bilibili.com/video/BV12A4y1Z7LP)

状态： 3分钟 AC, java + python

思路: 双指针
左右指针同时指向0， 用右指针遍历数组，发现相同的值则跳过，right++, 否则复制值到左指针，左右指针都自加1

Java:
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int left = 0;
        int right = 0;
        while(right < nums.length){
            if(nums[right] == val){
                right++;
            }else{
                nums[left++] = nums[right++];
            }
        }
        return left;
    }
}
```
Python3:
```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        right = 0
        while right < len(nums):
            if nums[right] == val:
                right += 1
            else:
                nums[left] = nums[right]
                left += 1
                right += 1
        return left
```

总结：

704 题， 注意binary search only works for  **SORTED** list/array
 1.  iteration 比 recursion 要简单直接， recursion要注意结束条件是小于而不是小于等于，因为存在left==right==mid, 同时 target 刚好等于nums[mid] 的情况
 2.  看题目要求，要求的是返回index，所以不能切割int array作为新参数，否则index就乱了，但如果是判断是否存在，则可以直接切割array，就不用left和right了。

27 题，
 1.  比较简单，无总结

