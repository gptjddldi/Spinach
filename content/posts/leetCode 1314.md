---
title: "1314. Matrix Block Sum"
date: 2023-03-11T22:02:37+09:00
draft: false
---

```python
class Solution:
    def matrixBlockSum(self, mat: List[List[int]], k: int) -> List[List[int]]:
        M,N = len(mat), len(mat[0])
        dp = [[0 for _ in range(N)] for _ in range(M)]
        dp[0][0] = mat[0][0]
        for i in range(1,M):
            dp[i][0] = dp[i-1][0] + mat[i][0]
        for j in range(1,N):
            dp[0][j] = dp[0][j-1] + mat[0][j]

        for i in range(1,M):
            for j in range(1,N):
                dp[i][j] = dp[i-1][j] + dp[i][j-1] - dp[i-1][j-1] + mat[i][j]
        
        ret = [[0 for _ in range(N)] for _ in range(M)]

        for i in range(M):
            for j in range(N):
                minI = max(i-k, 0)
                minJ = max(j-k, 0)
                maxI = min(i+k, M-1)
                maxJ = min(j+k, N-1)
                ret[i][j] = dp[maxI][maxJ]
                if minI > 0:
                    ret[i][j] -= dp[minI-1][maxJ]
                if minJ > 0:
                    ret[i][j] -= dp[maxI][minJ-1]
                if minI > 0 and minJ > 0:
                    ret[i][j] += dp[minI-1][minJ-1]
        return ret
```