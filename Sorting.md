# Leetcode

## [Leetcode 164. Maximum Gap](https://leetcode.com/problems/maximum-gap/)
Given an integer array nums, return the maximum difference between two successive elements in its sorted form. If the array contains less than two elements, return 0.
You must write an algorithm that runs in linear time and uses linear extra space.
Example:
```
Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.
```
### Code
```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        num = sorted(nums)
        maxGap = 0
        for x in range(len(num) - 1):
            maxGap = max(maxGap, num[x + 1] - num[x])
        return maxGap
```
![image](https://user-images.githubusercontent.com/69243911/128641027-07a8f55b-9d64-40df-b2f1-383fe7c89291.png)
