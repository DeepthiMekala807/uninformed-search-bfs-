from collections import deque
graph = {
    'A': ['B', 'C'],
    'B': ['C', 'D', 'E'],
    'C': ['E'],
    'D': ['E', 'F'],
    'E': ['F'],
    'F': []  
}


edge_costs = {
    ('A', 'B'): 4,
    ('A', 'C'): 5,
    ('B', 'C'): 11,
    ('B', 'D'): 9,
    ('B', 'E'): 7,
    ('C', 'E'): 3,
    ('D', 'E'): 13,
    ('D', 'F'): 2,
    ('E', 'F'): 6
}
def bfs(graph, start, target):
    visited = set()
    queue = deque()
    parent = {}  
    
    queue.append(start)
    visited.add(start)
    parent[start] = None
    
    while queue:
        current_node = queue.popleft()
        
        
        if current_node == target:
            path = []
            while current_node is not None:
                path.append(current_node)
                current_node = parent[current_node]
            return path[::-1]  
        
        for neighbor in graph[current_node]:
            if neighbor not in visited:
                visited.add(neighbor)
                parent[neighbor] = current_node
                queue.append(neighbor)
    
    return None  


path = bfs(graph, 'A', 'F')

if path:
    print("BFS Path from A to F:", ' -> '.join(path))
else:
    print("No path exists from A to F")
