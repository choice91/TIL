## BFS (Breadth First Search)
### 개념
- 한 노드를 시작으로 인접한 모든 정점을 우선 방문하는 방식 (현재 인접한 노드를 먼저 방문)
- 인접한 노드 중 방문하지 않은 모든 노드들을 저장해두고 가장 처음에 넣은 노드를 꺼내서 탐색 -> `Queue`를 사용
- 더 이상 방문하지 않은 정점이 없을 때까지 방문하지 않은 모든 정점들에 대해서도 넓이 우선 검색을 적용
### 장점
- 최단 경로를 쉽게 찾을 수 있다.
### 단점
- 모든 분기되는 수를 다 저장하다보니 공간을 많이 써야하고, 모든 걸 다 보고 오다보니 시간이 오래걸릴 수 있다.
```
graph = {
    1: [2, 3, 4],
    2: [1, 5],
    3: [1, 6, 7],
    4: [1, 8],
    5: [2, 9],
    6: [3, 10],
    7: [3],
    8: [4],
    9: [5],
    10: [6]
}

def bfs(graph, start):
    queue = [start]
    visited = []
    while queue:
        print(queue)
        cur_node = queue.pop(0)
        visited.append(cur_node)
        for node in graph[cur_node]:
            if node not in visited:
                queue.append(node)
    return visited

print(bfs(graph, 1))
# 결과 : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
### 순서
1. 시작노드를 큐에 넣음
2. 현재 큐의 노드를 빼서 visited에 추가
3. 현재 방문한 노드와 인접한 노드 중 방문하지 않은 
