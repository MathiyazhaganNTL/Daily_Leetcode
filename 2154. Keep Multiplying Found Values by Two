class Solution(object):
    def findFinalValue(self, nums, original):
        memo = [False] * 1001
        for x in nums:
            if x <= 1000:
                memo[x] = True

        x = original
        while x <= 1000:
            if memo[x]:
                x *= 2
            else:
                break

        return x
