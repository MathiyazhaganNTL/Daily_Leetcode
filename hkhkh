class Solution:
    def smallestNumber(self, num: str, t: int) -> str:
        from collections import deque
        #Factor t into primes [2,3,5,7]
        primes = [2, 3, 5, 7]
        A = [0]*4
        tmp = t
        for i, p in enumerate(primes):
            while tmp % p == 0:
                A[i] += 1
                tmp //= p
        if tmp != 1:
            return "-1"
        A = tuple(A)

        #Precompute exponent vectors for digits 1 to 9
        exp_map = {}
        for d in range(1, 10):
            cnt = [0]*4
            x = d
            for i, p in enumerate(primes):
                while x % p == 0:
                    cnt[i] += 1
                    x //= p
            exp_map[d] = tuple(cnt)

        #Compute max exponent per prime across digits
        max_exp = [0]*4
        for d in range(1, 10):
            for i in range(4):
                max_exp[i] = max(max_exp[i], exp_map[d][i])

        #Helper to add and clamp exponent vectors
        def add(a, b):
            return tuple(min(a[i] + b[i], A[i]) for i in range(4))
        #Feasibility: can L digits cover needed vector N?
        def feasible(N, L):
            for i in range(4):
                if N[i] > max_exp[i] * L:
                    return False
            return True

        #Compute prefix contributions and zero-prefix flags
        n = len(num)
        prefix = [(0,0,0,0)] * (n+1)
        zero_pref = [False] * (n+1)
        cur = (0,0,0,0)
        for i, ch in enumerate(num):
            zero_pref[i+1] = zero_pref[i] or (ch == '0')
            if ch != '0':
                cur = add(cur, exp_map[int(ch)])
            prefix[i+1] = cur

        #Check if original number already satisfies
        if not zero_pref[n] and prefix[n] == A:
            return num

        #Build DP via BFS over exponent-state space
        start = (0,0,0,0)
        dp = {start: 0}
        prev = {}
        choice = {}
        q = deque([start])
        while q:
            s = q.popleft()
            for d in range(2, 10):
                ns = add(s, exp_map[d])
                if ns not in dp:
                    dp[ns] = dp[s] + 1
                    prev[ns] = s
                    choice[ns] = d
                    q.append(ns)

        #Try to modify at each suffix position (same-length)
        for i in range(n-1, -1, -1):
            if zero_pref[i]:
                continue
            base = prefix[i]
            orig = int(num[i])
            for d in range(orig+1, 10):
                new_pref = add(base, exp_map[d])
                need = tuple(A[j] - new_pref[j] for j in range(4))
                L = n - (i + 1)
                if not feasible(need, L):
                    continue

                #Find minimal dp state covering `need`
                best_state = None
                best_cnt = float('inf')
                for st, cnt in dp.items():
                    if all(st[j] >= need[j] for j in range(4)) and cnt < best_cnt:
                        best_cnt = cnt
                        best_state = st
                if best_state is None:
                    continue

                #Reconstruct digits for suffix
                digs = []
                s = best_state
                while s != start:
                    digs.append(str(choice[s]))
                    s = prev[s]
                #If too many digits needed, cannot fit same-length
                if len(digs) > L:
                    continue
                digs.sort()
                suffix = '1' * (L - len(digs)) + ''.join(digs)
                return num[:i] + str(d) + suffix

        #If no same-length solution, build smallest (n+1)-digit number
        L = n + 1
        # choose minimal multiset of digits covering A
        best_state = None
        best_cnt = float('inf')
        for st, cnt in dp.items():
            if all(st[i] >= A[i] for i in range(4)) and cnt < best_cnt:
                best_cnt = cnt
                best_state = st
        if best_state is None:
            return "-1"

        digs = []
        s = best_state
        while s != start:
            digs.append(str(choice[s]))
            s = prev[s]
        digs.sort()
        # fill with leading '1's
        result = '1' * (L - len(digs)) + ''.join(digs)
        return result
