# 二分搜索
## 二分搜索模板
给一个**有序数组**和目标值，找第一次/最后一次/任何一次出现的索引，如果没有出现返回-1

模板四点要素

- 1、初始化：start=0、end=len-1
- 2、循环退出条件：start + 1 < end
- 3、比较中点和目标值：A[mid] ==、 <、> target
- 4、判断最后两个元素是否符合：A[start]、A[end] ? target

时间复杂度 O(logn)，使用场景一般是有序数组的查找

## 例子
**binary-search**
- mode 1
二分查找最基础最基本的形式
查找条件可以在不与元素两侧比较的情况下确定
不需要后处理，每一步都会检查是否找到了元素
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while(left <= right){
            int mid = (right - left)/2 + left;
            int num = nums[mid];
            if(num == target){
                return mid;
            }
            else if(num < target){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }
        return -1;
    }
}
- mode 2
二分查找高级方法
访问元素的直接右邻居
使用元素的右邻居来决定向左还是向右
保证查找空间每一步至少有2个元素
需要进行后处理，剩下一个元素循环递归结束，需要评估剩余元素是否满足条件
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length;
        while(left < right){
            int mid = (right - left)/2 + left;
            int num = nums[mid];
            if(num == target){
                return mid;
            }
            else if(num < target){
                left = mid + 1;
            }
            else{
                right = mid;
            }
        }
        return -1;
    }
}
- mode 3
实现二分查找的另一种方法
搜索条件需要访问元素的直接左右邻居
使用元素的邻居来确定向左还是向右
保证查找空间每个步骤至少有3个元素
需要进行后处理，剩下2个元素循环/递归结束，需要评估剩余元素是否符合条件
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while(left <= right){
            int mid = (right - left)/2 + left;
            int num = nums[mid];
            if(num == target){
                return mid;
            }
            else if(num < target){
                left = mid;
            }
            else{
                right = mid;
            }
        }
        return -1;
    }
}
