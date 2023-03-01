---
title: "LeetCode 128. Longest Consecutive Sequence"
date: 2023-03-01T23:18:30+09:00
draft: false
---

# time: O(N) / space: O(N)
``` python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        d = dict()
        if not nums:
            return 0
        for num in nums:
            if num in d:
                continue
            l,r = num-1, num+1
            left_value = d.get(l, 0)
            right_value = d.get(r, 0)
            d[num] = left_value + right_value + 1
            d[num-left_value] = d[num]
            d[num+right_value] = d[num]
        return max(d.values())
```
양 옆 끝의 값을 업데이트 하면서 진행
:laughing:
