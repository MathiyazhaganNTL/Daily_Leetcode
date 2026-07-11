class Solution:
    def countCompleteComponents(self, n: int, edges: List[List[int]]) -> int:
        adj = [[] for _ in range(n)]

        for u, v in edges:
            adj[u].append(v)
            adj[v].append(u)

        vis = [False] * n
        ans = 0

        for i in range(n):
            if vis[i]:
                continue

            queue = deque([i])
            vis[i] = True

            nodes = 0       # Number of nodes in the component
            edge_count = 0  # Sum of degrees in the component

            while queue:
                u = queue.popleft()

                nodes += 1
                edge_count += len(adj[u])

                for v in adj[u]:
                    if not vis[v]:
                        vis[v] = True
                        queue.append(v)

            edge_count //= 2

            if edge_count == nodes * (nodes - 1) // 2:
                ans += 1

        return ans
