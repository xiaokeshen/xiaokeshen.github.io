# Problem  
-[886. Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)

# Solution 
This is a classicial bipartition problem. We can use the DFS algorithm to solve the problem. Basic idea is building the graph based on the dislike edges. Then the dislike edges will build a graph and we can do it by using DFS. In this graph, the dislike relationship will be represented as we are using bipartition graph. If we can finally build a DFS forest where each tree is bipartition, we return True. If we have any confilict, we return False.  

Also, it is not necessary to be a tree for each bipartition graph. Even a loop graph can be implemented by using this algorithm.

- DFS code 1

```python
# time complexity: O(V+E)
# Space complexity: O(V+bd) where b is the average brach for each node and d is the depth of the DFS search tree.
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        def dfs(i):
            open_list = [i]
            colors[i] = 1
            while open_list:
                i = open_list.pop()
                for v in connections[i]:
                    if v in colors:
                        if colors[v] != -colors[i]:return False
                    else:
                        colors[v] = -colors[i]
                        open_list.append(v)
            return True
        connections = collections.defaultdict(list)
        for a, b in dislikes:
            connections[a].append(b)
            connections[b].append(a)
        colors = {}
        for i in range(1, N+1):
            if i not in colors and not dfs(i):return False
        return True
```

- DFS code 2  

```python
# time complexity: O(V+E)
# Space complexity: O(V+bd) where b is the average brach for each node and d is the depth of the DFS search tree.
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        colors = {}
        graph = collections.defaultdict(list)
        for a,b in dislikes:
            graph[a-1].append(b-1)
            graph[b-1].append(a-1)
            
        def dfs(i, color):
            colors[i] = color
            for j in graph[i]:
                if j in colors:
                    if colors[j]!= (not color):return False
                else:
                    if not dfs(j, not color):return False
            return True
        for i in range(N):
            if i not in colors:
                if not dfs(i, False):return False
        return True
```

