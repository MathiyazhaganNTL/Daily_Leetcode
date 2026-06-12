class Solution:
    def assignEdgeWeights(self, edges: List[List[int]], queries: List[List[int]]) -> List[int]:
        g, q = defaultdict(set), defaultdict(set)
        for u, v in edges:
            g[u].add(v)
            g[v].add(u)
        for u, v in queries:
            q[u].add(v)
            q[v].add(u)

        dis, lca, fa = {}, {}, list(range(len(g)+1))
        def find(x):
            if x!=fa[x]:
                fa[x] = find(fa[x])
            return fa[x]
        def tarjan(u, d):
            dis[u] = d
            for v in g[u]:
                if v not in dis:
                    tarjan(v, d+1)
                    fa[v] = u
            for v in q[u]:
                if v in dis:
                    lca[(u, v)] = lca[(v, u)] = find(v)

        tarjan(1, 0)
        p, mod = [0, 1], (10**9+7)
        edges_x = [dis[x]+dis[y]-2*dis[lca[(x, y)]] for x, y in queries]
        for _ in range(max(edges_x)):
            p.append((p[-1]*2)%mod)
        return [p[i] for i in edges_x]
