## DFS
### 개념
- 깊이 우선 탐색 (Depth First Search)
- 트리나 그래프에서 한 루트로 탐색하다가 특정 상황에서 최대한 깊숙히 들어가서 확인한 뒤 다시 돌아가 다른 루트로 탐색하는 방식
- 일반적으로 `재귀호출`을 사용하여 구현하지만, `스택`으로도 구현할 수 있다.
- 그래프의 최대 깊이 만큼의 공간을 요구하기 때문에 공간을 적게 씀.
- 최단 경로를 탐색하기 쉽지 않다.

![220px-Depth-First-Search](https://user-images.githubusercontent.com/48742487/122945016-3b27c180-d3b3-11eb-97ce-78d5271426c9.gif)

이미지출처 https://ko.wikipedia.org/wiki/%EA%B9%8A%EC%9D%B4_%EC%9A%B0%EC%84%A0_%ED%83%90%EC%83%89


### 재귀호출을 사용하여 구현
```
graph = {
    1: [2, 5, 9],
    2: [1, 3],
    3: [2, 4],
    4: [3],
    5: [1, 6, 8],
    6: [5, 7],
    7: [6],
    8: [5],
    9: [1, 10],
    10: [9]
}
visited = []

def dfs(graph, cur_node, visited):
    visited.append(cur_node)
    
    for node in graph:
        if node not in visited:
            dfs(graph, node, visited)

dfs(graph, 1, visited)
print(visited)
```
1. 시작노드(루트노드)인 1부터 탐색시작
2. 현재 방문한 노드를 visited에 추가
3. 현재 방문한 노드와 인접한 노드 중 방문하지 않은 노드에 방문
