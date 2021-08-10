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

### Code_2(bucketsort)
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

### Code_3(Radix Sort)
![image](https://user-images.githubusercontent.com/69243911/128853907-1e9040df-3e9d-4bb2-8d11-4ea3537680bb.png)
![image](https://user-images.githubusercontent.com/69243911/128853799-393fcfcc-5065-4dbb-a17e-2a7e22373375.png)
![image](https://user-images.githubusercontent.com/69243911/128853867-e7444aa9-68e5-463d-9af2-1b2589b4f6b7.png)
```python
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        def countingSort(inputArray):
            # Find the maximum element in the inputArray
            maxEl = max(inputArray)

            countArrayLength = maxEl+1

            # Initialize the countArray with (max+1) zeros
            countArray = [0] * countArrayLength

            # Step 1 -> Traverse the inputArray and increase 
            # the corresponding count for every element by 1
            for el in inputArray: 
                countArray[el] += 1

            # Step 2 -> For each element in the countArray, 
            # sum up its value with the value of the previous 
            # element, and then store that value 
            # as the value of the current element
            for i in range(1, countArrayLength):
                countArray[i] += countArray[i-1] 

            # Step 3 -> Calculate element position
            # based on the countArray values
            outputArray = [0] * len(inputArray)
            i = len(inputArray) - 1
            while i >= 0:
                currentEl = inputArray[i]
                countArray[currentEl] -= 1
                newPosition = countArray[currentEl]
                outputArray[newPosition] = currentEl
                i -= 1

            return outputArray
        
        num = countingSort(nums)        
        maxGap = 0
        for x in range(len(num) - 1):
            maxGap = max(maxGap, num[x + 1] - num[x])
        return maxGap
```
