# GIỮA KÌ - NHẬP MÔN AI
[Đề bài](https://drive.google.com/file/d/1s0N8USjgXKULyc-W2lzqKV38pn7cKdvq/view?usp=sharing)
## I.  **Best First Search**


>### Data Structure:

Data có dạng là cac file txt: 

vd: test0.txt

```
1 1 0 0 0 
1 0 0 0 1
0 1 0 1 0
0 0 0 0 0 
1 0 1 0 1  
``` 



>### Code: 


```python
# Nguyen Trung Tin - 51900640
class Graph:
  def __init__(self, row, col, g):
    self.ROW = row
    self.COL = col
    self.graph = g


  def BFS(self, i, j):
    queue = []
    queue.append([i,j])
    self.graph[i][j] = -1
    # Toa do x,y cua 8 Node gan Current Node
    rowNbr = [-1, -1, -1, 0, 0, 1, 1, 1]
    colNbr = [-1, 0, 1, -1, 1, -1, 0, 1] 

		
    while queue: 
      s = queue.pop(0)
      # Kiem tra 8 Node canh current Node 
      for k in range(8):
        if s[0]+rowNbr[k] >= 0 and s[0]+rowNbr[k] < self.ROW 
        and s[1]+colNbr[k] >=0 and s[1]+colNbr[k] < self.COL 
        and self.graph[s[0]+rowNbr[k]][s[1]+colNbr[k]] == 1:
        
          self.graph[s[0]+rowNbr[k]][s[1]+colNbr[k]] = -1  
          queue.append([s[0]+rowNbr[k],s[1]+colNbr[k]])


  def countIslands(self):

    count = 0
    for i in range(self.ROW):
      for j in range(self.COL):
        if self.graph[i][j] == 1:
          self.BFS(i, j)
          count += 1

    return count
```
>### chuẩn bị input 

```python
import os  
# Folder Path
path = "Enter folder path"

os.chdir(path)
def read_text_file(file_path):
  with open(file_path, 'r') as f:
    graph = [[int(num) for num in line.split()] for line in f]
    return graph

for file in os.listdir():
  if file.endswith(".txt"):
      file_path = f"{path}/{file}"
      graph = read_text_file(file_path)
      
      row = len(graph)
      col = len(graph[0])

      g = Graph(row, col, graph)

      print (file,": ", g.countIslands())
```




> ### Test: 

* Test case 1:

test0.txt:
```
1 1 0 0 0 0 
1 0 0 1 0 1 
0 1 0 1 0 0 
0 0 0 0 0 0 
1 1 0 0 1 1 
```  
test1.txt: 
```
1 1 0 1 0 0 
1 0 0 0 0 1 
0 0 0 1 0 0 
0 0 0 0 0 0 
1 1 0 0 1 1 
```
test2.txt
```
1 1 0 0 0 0 
1 0 0 1 1 1 
0 1 0 1 0 0 
0 1 0 0 0 0 
1 1 0 0 1 1 
```

>**Kết quả**

```
test0.txt :  5
test1.txt :  6
test2.txt :  3
```



## II.  **Uniform cost Search (UCS)**

>### Data Structure:

Data có dạng là cac file txt: 

vd: test0.txt

```
1 1 0 0 0 
1 0 0 0 1
0 1 0 1 0
0 0 0 0 0 
1 0 1 0 1  
``` 



>### Code: 


```python
# Nguyen Trung Tin - 51900640
def sortQueue(queue, cost):
  marklist = sorted((value, key) for (key,value) in cost.items())
  sortdict = dict([(k,v) for v,k in marklist])
  results = []
  for i in sortdict: 

    if [i[0],i[1]] in queue: 
      results.append([i[0],i[1]])
  return results
class Graph:
  def __init__(self, row, col, g):
    self.ROW = row
    self.COL = col
    self.graph = g




  def UCS(self, i, j):
    queue = []
    queue.append([i,j])
    self.graph[i][j] = -1
    rowNbr = [-1, -1, -1, 0, 0, 1, 1, 1]
    colNbr = [-1, 0, 1, -1, 1, -1, 0, 1] 
    cost = {(i,j):0}

    while queue: 
      queue = sortQueue(queue, cost)
      s = queue.pop(0)
      for k in range(8):
        if s[0]+rowNbr[k] >= 0 and s[0]+rowNbr[k] < self.ROW and s[1]+colNbr[k] >=0 and s[1]+colNbr[k] < self.COL and self.graph[s[0]+rowNbr[k]][s[1]+colNbr[k]] == 1:
          cost.update({(s[0]+rowNbr[k], s[1]+colNbr[k]): cost[(s[0],s[1])] + 1})  
          self.graph[s[0]+rowNbr[k]][s[1]+colNbr[k]] = -1
          queue.append([s[0]+rowNbr[k],s[1]+colNbr[k]])



  def countIslands(self):
   

    count = 0
    for i in range(self.ROW):
      for j in range(self.COL):
        if self.graph[i][j] == 1:
          self.UCS(i, j)
          count += 1

    return count

```
>### chuẩn bị input 
```python
import os  
# Folder Path
path = "Enter folder path"

os.chdir(path)
def read_text_file(file_path):
  with open(file_path, 'r') as f:
    graph = [[int(num) for num in line.split()] for line in f]
    return graph

for file in os.listdir():
  if file.endswith(".txt"):
      file_path = f"{path}/{file}"
      graph = read_text_file(file_path)
      
      row = len(graph)
      col = len(graph[0])

      g = Graph(row, col, graph)

      print (file,": ", g.countIslands())
```




> ### Test: 

- Test case 1

_test0.txt_
```
1 1 0 0 0 0 
1 0 0 1 0 1 
0 1 0 1 0 0 
0 0 0 0 0 0 
1 1 0 0 1 1 
```  

- Test case 2

_test1.txt_
```
1 1 0 1 0 0 
1 0 0 0 0 1 
0 0 0 1 0 0 
0 0 0 0 0 0 
1 1 0 0 1 1 
```
- Test case 3

_test2.txt_
```
1 1 0 0 0 0 
1 0 0 1 1 1 
0 1 0 1 0 0 
0 1 0 0 0 0 
1 1 0 0 1 1 
```

>**Kết quả**

```
test0.txt :  5
test1.txt :  6
test2.txt :  3
```







## III.  **Gready best first search**


>### Data Structure:

Data có dạng là cac file txt: 

1. file Graph.txt chứa: 
    * điểm bắt đầu 
    * điểm đến 
    * khoảng cách giữa các điểm 

```
20 23
Arad
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
``` 
2. file Heuristic.txt: 
    * chứa độ dài chim bay các điểm tới điểm đích: 

```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```


>### Code: 



* ### Hàm Gready best first search

```python
cost = {start: 0}             # cost là tổng weight của mỗi cạnh từ điểm bắt đầu đến điểm đó


def GBFS():
    global graph, heuristic
    closed = []             # closed nodes
    opened = [[start, 366]]     # opened nodes
    

    '''A star Search'''
    while True:
        fn = [i[1] for i in opened]     
        chosen_index = fn.index(min(fn))
        node = opened[chosen_index][0]  # current node
        
        closed.append(opened[chosen_index])
        
        if closed[-1][0] == dest:        # dừng vòng lặp tới khi tìm được đích đến (Bucharest)
            break
        del opened[chosen_index]
        for neighbor in graph[node]:
            
            if neighbor[0] not in [closed_item[0] for closed_item in closed]: 
              costTmp = cost[node] + neighbor[1]
              if neighbor[0] in [opened_item[0] for opened_item in opened]:
              # Nếu node nằm trong opened lại có cost mới thấp hơn thì thay thế bằng cost mới. 
                if costTmp < cost[neighbor[0]]:
                  cost.update({neighbor[0]: costTmp})  
              else: 
                  cost.update({neighbor[0]: costTmp})

              fn_node = heuristic[neighbor[0]] # fn = f(n) =  h(n)
              opened.append([neighbor[0], fn_node])  
        
    '''find optimal path'''
    trace_node = dest                        
    path_result = [dest]               

    for i in range(len(closed)-2, -1, -1):
        check_node = closed[i][0]           # current node
        if trace_node in [children[0] for children in graph[check_node]]:
            children_costs = [temp[1] for temp in graph[check_node]]
            children_nodes = [temp[0] for temp in graph[check_node]]
         
            
            # Tìm nếu cost của Node  + cost của Node_Neighbor = cost đích 
            # thì Node_Neighbor nằm trong đường đi chính xác. 

            if cost[check_node] + children_costs[children_nodes.index(trace_node)] == cost[trace_node]:
                path_result.append(check_node)
                trace_node = check_node
    path_result.reverse()              # reverse the optimal sequence

    return closed, path_result


if __name__ == '__main__':
    visited_nodes, optimal_nodes = GBFS()
    print('visited nodes: ' + str(visited_nodes))
    print('optimal nodes sequence: ' + str(optimal_nodes))
```
* Chuẩn bị input: 
```python
# Nguyen Trung Tin - 51900640
'''Hàm đọc graph.txt + build graph'''
def build_graph(file):

  # Chuyển dữ liệu từ file txt sang dictionary
    graph = {}
    for line in file:
        v1, v2, w = line.split(',')
        v1 = v1.strip()
        v2 = v2.strip()
        w = int(w.strip())
        if v1 not in graph:  
            graph[v1] = []
        if v2 not in graph:  
            graph[v2] = []
        graph[v1].append([v2,w])
        graph[v2].append([v1,w])
    return graph
with open('Graph.txt', 'r') as file:
    lines = file.readlines()

start = lines[1].strip() # Line 1 sẽ là điểm bắt đầu
dest = lines[2].strip()  # Line 2 sẽ là điểm đến 
graph = build_graph(lines[4:])  # Khoảng cách giữa 2 điểm sẽ từ line 4 trở đi 

# print(graph)

'''Hàm đọc heuristic.txt và build heuristic '''
def build_heuristic():
    h = {}
    with open("Heuristic.txt", 'r') as file:
        for line in file:
            line = line.strip().split(",")
            node = line[0].strip()
            sld = int(line[1].strip())
            h[node] = sld
    return h

heuristic = build_heuristic()

# for key,value in h.items():
# 	print(key, ':', value)
```



> ### Test: 

- Test case 1

_Graph.txt_
```
20 23
Arad
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Arad', 366], ['Sibiu', 253], ['Fagaras', 176], ['Bucharest', 0]]
optimal nodes sequence: ['Arad', 'Sibiu', 'Fagaras', 'Bucharest']
```

- Test case 2

_Graph.txt_
```
20 23
Dobreta
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Dobreta', 366], ['Craiova', 160], ['Pitesti', 100], ['Bucharest', 0]]
optimal nodes sequence: ['Dobreta', 'Craiova', 'Pitesti', 'Bucharest']
```
- Test case 3

_Graph.txt_
```
20 23
Oradea
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Oradea', 366], ['Sibiu', 253], ['Fagaras', 176], ['Bucharest', 0]]
optimal nodes sequence: ['Oradea', 'Sibiu', 'Fagaras', 'Bucharest']
```
## III.  **A Star Search**


>### Data Structure:

Data có dạng là cac file txt: 

1. file Graph.txt chứa: 
    * điểm bắt đầu 
    * điểm đến 
    * khoảng cách giữa các điểm 

```
20 23
Arad
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
``` 
2. file Heuristic.txt: 
    * chứa độ dài chim bay các điểm tới điểm đích: 

```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```


>### Code: 



* ### Hàm A Star Search

```python
cost = {start: 0}             # cost là tổng weight của mỗi cạnh từ điểm bắt đầu đến điểm đó


def AStar():
    global graph, heuristic
    closed = []             # closed nodes
    opened = [[start, 366]]     # opened nodes
    

    '''A star Search'''
    while True:
        fn = [i[1] for i in opened]     
        chosen_index = fn.index(min(fn))
        node = opened[chosen_index][0]  # current node
        
        closed.append(opened[chosen_index])
        
        if closed[-1][0] == dest:        # dừng vòng lặp tới khi tìm được đích đến (Bucharest)
            break
        del opened[chosen_index]
        for neighbor in graph[node]:
            
            if neighbor[0] not in [closed_item[0] for closed_item in closed]: 
              costTmp = cost[node] + neighbor[1]
              if neighbor[0] in [opened_item[0] for opened_item in opened]:
              # Nếu node nằm trong opened lại có cost mới thấp hơn thì thay thế bằng cost mới. 
                if costTmp < cost[neighbor[0]]:
                  cost.update({neighbor[0]: costTmp})  
              else: 
                  cost.update({neighbor[0]: costTmp})

              fn_node = costTmp  + heuristic[neighbor[0]] # fn = f(n) = g(n) + h(n)
              opened.append([neighbor[0], fn_node])  
        
    '''find optimal path'''
    trace_node = dest                        
    path_result = [dest]               

    for i in range(len(closed)-2, -1, -1):
        check_node = closed[i][0]           # current node
        if trace_node in [children[0] for children in graph[check_node]]:
            children_costs = [temp[1] for temp in graph[check_node]]
            children_nodes = [temp[0] for temp in graph[check_node]]
         
            
            # Tìm nếu cost của Node  + cost của Node_Neighbor = cost đích thì là đường đi chính xác. 

            if cost[check_node] + children_costs[children_nodes.index(trace_node)] == cost[trace_node]:
                path_result.append(check_node)
                trace_node = check_node
    path_result.reverse()              # reverse the optimal sequence

    return closed, path_result


if __name__ == '__main__':
    visited_nodes, optimal_nodes = AStar()
    print('visited nodes: ' + str(visited_nodes))
    print('optimal nodes sequence: ' + str(optimal_nodes))
```
* Chuẩn bị input: 
```python
# Nguyen Trung Tin - 51900640
'''Hàm đọc graph.txt + build graph'''
def build_graph(file):

  # Chuyển dữ liệu từ file txt sang dictionary
    graph = {}
    for line in file:
        v1, v2, w = line.split(',')
        v1 = v1.strip()
        v2 = v2.strip()
        w = int(w.strip())
        if v1 not in graph:  
            graph[v1] = []
        if v2 not in graph:  
            graph[v2] = []
        graph[v1].append([v2,w])
        graph[v2].append([v1,w])
    return graph
with open('Graph.txt', 'r') as file:
    lines = file.readlines()

start = lines[1].strip() # Line 1 sẽ là điểm bắt đầu
dest = lines[2].strip()  # Line 2 sẽ là điểm đến 
graph = build_graph(lines[4:])  # Khoảng cách giữa 2 điểm sẽ từ line 4 trở đi 

# print(graph)

'''Hàm đọc heuristic.txt và build heuristic '''
def build_heuristic():
    h = {}
    with open("Heuristic.txt", 'r') as file:
        for line in file:
            line = line.strip().split(",")
            node = line[0].strip()
            sld = int(line[1].strip())
            h[node] = sld
    return h

heuristic = build_heuristic()

# for key,value in h.items():
# 	print(key, ':', value)
```



> ### Test: 

- Test case 1

_Graph.txt_
```
20 23
Arad
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Arad', 366], ['Sibiu', 393], ['Rimnicu Vilcea', 413], ['Fagaras', 415], ['Pitesti', 417], ['Bucharest', 418]]
optimal nodes sequence: ['Arad', 'Sibiu', 'Rimnicu Vilcea', 'Pitesti', 'Bucharest']
```

- Test case 2

_Graph.txt_
```
20 23
Dobreta
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Dobreta', 366], ['Craiova', 280], ['Mehadia', 316], ['Pitesti', 358], ['Bucharest', 359]]
optimal nodes sequence: ['Dobreta', 'Craiova', 'Pitesti', 'Bucharest']
```
- Test case 3

_Graph.txt_
```
20 23
Oradea
Bucharest

Arad, Zerind, 75
Arad, Sibiu, 140
Arad, Timisoara, 118
Zerind, Oradea, 71
Oradea, Sibiu, 151
Timisoara, Lugoj, 111
Sibiu, Fagaras, 99
Sibiu, Rimnicu Vilcea, 80
Lugoj, Mehadia, 70
Fagaras, Bucharest, 211
Rimnicu Vilcea, Pitesti, 97
Rimnicu Vilcea, Craiova, 146
Mehadia, Dobreta, 75
Bucharest, Pitesti, 101
Bucharest, Urziceni, 85
Bucharest, Giurglu, 90
Pitesti, Craiova, 138
Craiova, Dobreta, 120
Urziceni, Hirsova, 98
Urziceni, Vaslui, 142
Hirsova, Eforie, 86
Vaslui, Lasi, 92
Lasi, Neamt, 87
```  

_Heuristic.txt_
```
Arad, 366
Bucharest, 0
Craiova, 160
Dobreta, 242
Eforie, 161
Fagaras, 176
Giurgiu, 77
Hirsowa, 151
Lasi, 226
Lugoj, 244
Mehadia, 241
Neamt, 234
Oradea, 380
Pitesti, 100
Rimnicu Vilcea, 193
Sibiu, 253
Timisoara, 329
Urziceni, 80
Vaslui, 199
Zerind, 374
```

>Kết quả: 

```
visited nodes: [['Oradea', 366], ['Sibiu', 404], ['Rimnicu Vilcea', 424], ['Fagaras', 426], ['Pitesti', 428], ['Bucharest', 429]]
optimal nodes sequence: ['Oradea', 'Sibiu', 'Rimnicu Vilcea', 'Pitesti', 'Bucharest']
```







