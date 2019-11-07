# 665. Non-decreasing Array

This problem is like a greedy problem. When you find `nums[i-1] > nums[i]` for some `i`, you will prefer to change `nums[i-1]`'s value, since a larger `nums[i]` will give you more risks that you get inversion errors after position `i`. But, if you also find `nums[i-2] > nums[i]`, then you have to change `nums[i]`'s value instead, or else you need to change both of `nums[i-2]`'s and `nums[i-1]`'s values.

```text
class Solution(object):    def checkPossibility(self, nums):        """        :type nums: List[int]        :rtype: bool        """        count = 0        for i in range(1,len(nums)):            if nums[i-1] > nums[i]:                count += 1                if i - 2 >= 0 and nums[i-2] > nums[i]:                    nums[i] = nums[i-1]                else:                    nums[i-1] = nums[i]        return count <= 1
```

