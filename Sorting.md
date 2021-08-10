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
### Code_1
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

### Code_2
```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        def bucketsort(data):
            max_score = 1000000000
            bucket = []
    
            for i in range(max_score+1):
                bucket.append(0)
            for score in data:
                bucket[score] = bucket[score] + 1

            index = 0
            for i in range(len(bucket)):
                if bucket[i] != 0:
                    for j in range(bucket[i]):
                        data[index] = i
                        index += 1
        
        bucketsort(nums)        
        maxGap = 0
        for x in range(len(nums) - 1):
            maxGap = max(maxGap, nums[x + 1] - nums[x])
        return maxGap
```
![image](https://user-images.githubusercontent.com/69243911/128853169-33167ec7-9e60-47d7-85f8-768f0fd95cc1.png)
