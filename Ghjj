# Added using AI
class Solution:
    def numberOfSpecialChars(self, word: str) -> int:
        mpl = [-1] * 26
        mpu = [-1] * 26
        for i, a in enumerate(word) :
            if a.islower():
                mpl[ord(a) - ord('a')] = i
            else:
                idx = ord(a) - ord('A')
                if mpu[idx] == -1 :
                    mpu[idx] = i
        ans = 0
        for i in range(26) :
            if mpl[i] != -1 and mpu[i] != -1:
                if mpl[i] < mpu[i]:
                    ans += 1
        return ans
