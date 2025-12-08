## [Wiggle Sort](https://www.lintcode.com/problem/508/)

<!-- notecardId: 1765122718810 -->

```python
# Explanation:
# - Neetcode: https://youtu.be/vGsyTE4s34w

# Type: Unstable

# - Time: O(n log (n))
# - Space: O(1)
from typing import List

class Solution:
    def wiggle_sort(self, nums: List[int]):
        nums.sort()

        for i in range(1, len(nums) - 1, 2):
            nums[i], nums[i + 1], = nums[i + 1], nums[i]
```
