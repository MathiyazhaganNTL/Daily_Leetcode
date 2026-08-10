class Solution:
    def winnerSquareGame(self, n: int) -> bool:
        # dp[i] indicates if the player with 'i' stones remaining can win
        dp = [False] * (n + 1)
        
        # Precompute all perfect squares <= n to avoid redundant multiplication in inner loops
        squares = [j * j for j in range(1, int(n ** 0.5) + 1)]
        
        for i in range(1, n + 1):
            for sq in squares:
                if sq > i:
                    break
                # If taking 'sq' stones leaves the opponent in a losing state (False),
                # the current player can force a win from state 'i'.
                if not dp[i - sq]:
                    dp[i] = True
                    break
                    
        return dp[n]
