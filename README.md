# leetcode-problem-solving-
class Solution {
    public List<List<Integer>> getAncestors(int n, int[][] edges) {
                List<List<Integer>> ans = new ArrayList<>(n);
        List<List<Integer>> graph = new ArrayList<>(n);

        for (int i = 0; i < n; ++i) {
            ans.add(new ArrayList<>());
            graph.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            graph.get(u).add(v);
        }

        for (int i = 0; i < n; ++i) {
            dfs(graph, i, i, new boolean[n], ans);
        }

        for (int i = 0; i < n; ++i) {
            Collections.sort(ans.get(i));
        }

        return ans;
    }

    private void dfs(List<List<Integer>> graph, int u, int ancestor, boolean[] seen, List<List<Integer>> ans) {
        seen[u] = true;
        for (int v : graph.get(u)) {
            if (seen[v]) {
                continue;
            }
            ans.get(v).add(ancestor);
            dfs(graph, v, ancestor, seen, ans);
        }

    }
}
