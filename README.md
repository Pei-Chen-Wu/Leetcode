# Leetcode

## [Leetcode 1262. Greatest Sum Divisible by Three](https://leetcode.com/problems/greatest-sum-divisible-by-three/)
Example:
```
Input: nums = [3,6,5,1,8]
Output: 18
Explanation: Pick numbers 3, 6, 1 and 8 their sum is 18 (maximum sum divisible by 3).
```
### Code
```python
class Solution:
    def maxSumDivThree(self, nums: List[int]) -> int:
        #判斷內容物的性質
        a = [x for x in nums if x % 3 == 0] #三的倍數
        b = sorted([x for x in nums if x % 3 == 1], reverse=True) #除以三餘一，並反向排序
        c = sorted([x for x in nums if x % 3 == 2], reverse=True) #除以三餘二，並反向排序
        total = sum(nums)
        ans = 0
        #判斷最終答案
        if total % 3 == 0:  #總和剛好為三倍數
            ans = total
        if total % 3 == 1:
            if len(b) >= 1:     #減少一個餘數為1的內容物
                ans = max(ans, total - b[-1])
            if len(c) >= 2:     #減少兩個餘數為2的內容物
                ans = max(ans, total - sum(c[-2:]))
        elif total % 3 == 2:    
            if len(b) >= 2:     #減少兩個餘數為1的內容物
                ans = max(ans, total - sum(b[-2:]))
            if len(c) >= 1:     #減少一個餘數為2的內容物
                ans = max(ans, total - c[-1])

        return ans
```
![image](https://user-images.githubusercontent.com/69243911/126322365-9f45516c-a745-4264-b0da-49a3f2903c06.png)


## [Leetcode 1. Two Sum](https://leetcode.com/problems/two-sum/)

Example:
```
Input: nums = [3,6,5,1,1010], target = 7
Output: [1,3]
```
### Code
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            num2 = nums[i+1:]           #防止重複 
            for j in range(len(num2)):
                if (nums[i] + num2[j]) == target:
                    return i, j+i+1
```
![image](https://user-images.githubusercontent.com/69243911/126322610-cf6d57e0-daba-450c-922f-a64740554438.png)

## [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)
Example:
```
Input: nums = [1,2,0]
Output: 3
```
### Code_1
逐筆檢查 
```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        i = 1
        while True:
            if i not in nums:
                return i
            i += 1
```
![image](https://user-images.githubusercontent.com/69243911/127019290-4c3dc49d-cea8-4f67-97c1-58e035c7ff2a.png)

### Code_2
* 如果數組的長度是L，那麼結果最大就是L+1
* 給數組加一個0（處理0的情況），把長度令為l
* 把所有負數和大於等於l的數，都變成0
* 遍歷數組，把數對應下標的數加上l(把陣列位置當作數字是否出現過)
* (所以現在陣列內數字不重要)
* 再遍歷一遍，第一個小於l的數，他的位置i就是結果(代表那個位置沒有出現過)
* 但如果沒有小於l的數，結果就為l
![image](https://user-images.githubusercontent.com/69243911/127035902-3f8779ed-4728-4999-8042-222a28a2858c.png)

```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums.append(0)
        l = len(nums)
        if l == 1:   #代表無輸入
            return 1
        for i in range(l):
            if nums[i] < 0 or nums[i] >= l:
                nums[i] = 0
        for i in range(l):
            nums[nums[i] % l] += l
        for i in range(1, l):
            if nums[i] < l:
                return i
        return l
```
![image](https://user-images.githubusercontent.com/69243911/127019341-cde7cdc6-555c-4e62-a449-1e47d7e1dc5f.png)

## [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
Example:
![image](https://user-images.githubusercontent.com/69243911/128008569-f27b865c-a723-4016-886f-9d76d9987aa7.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```
### Code_1
1. 運行循環直到遍歷數組中的所有柱。 
2. 在當前柱的左側找到最大值。將此值設為 left_max。
3. 在當前柱的右側找到最大值。將此值設為 right_max。
4. 找到 left_max 和 right_max 之間的最小值。
5. 從當前柱中減去最小值。
6. 如果結果值大於 0，則將其添加到我們的結果中。由於我們不能有負數量的水被困，我們忽略它。
```python
class Solution:
    def trap(self, height: List[int]) -> int: 
        total_water = 0 
        for i in range(1, len(height)-1): 
            l = max(height[:i]) 
            r = max (height[i+1:]) 
            water = min(l, r) - height[i] 
            if(water>=0): 
                total_water += water 
        return total_water
```
![image](https://user-images.githubusercontent.com/69243911/128019570-876ace64-2976-4e32-83b9-2c232eecb4ff.png)

