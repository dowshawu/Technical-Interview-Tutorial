# Wiggle Sort

[Leetcode](https://leetcode.com/problems/wiggle-sort/)

題意：

Given an unsorted array nums, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

For example, given nums = [3, 5, 2, 1, 6, 4], one possible answer is [1, 6, 2, 5, 3, 4].


解題思路：

i等於偶數時，找最小的來換，奇數時，找最大的來換，花O(N^2)。

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        if (nums == null || nums.length < 2) {
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            int candidate = i;
            for (int j = i; j < nums.length; j++) {
                if (i % 2 == 0) {
                    if (nums[j] < nums[candidate]) {
                        candidate = j;
                    }
                } else {
                    if (nums[j] > nums[candidate]) {
                        candidate = j;
                    }
                }
            }
            int temp = nums[i];
            nums[i] = nums[candidate];
            nums[candidate] = temp;
        }
    }
}
```