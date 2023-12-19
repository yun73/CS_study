# Tree

<br>

## 트리란 ?

- 비선형 구조

- 원소들 간에 1 : N 관계를 갖는 자료구조

- 원소들 간에 계층관계를 갖는 계층형 자료구조

- 상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무) 모양의 구조

    <img src="https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png">


### 트리의 특징

- 한 개 이상의 노드로 이루어진 유한 집합이며, 다음 조건을 만족한다.

    - `노드 중 최상위 노드를 "루트(root) 노드" 라고 한다.`

    - `나머지 노드들은 n개의 분리 집합으로 분리될 수 있다.`

- 분리된 노드들은 각각 하나의 트리가 되며(재귀적 정의) 루트의 subtree(부트리)라 한다.

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image.png)


### 트리 용어 정리

<details>
<summary>용어 정리</summary>
<div markdown="1">

1. 노드(node) : 트리의 원소

2. 간선(edge) : 노드를 연결하는 선. 부모 노드와 자식 노드를 연결

3. 루트 노드(root) : 트리의 시작 노드

4. 형제 노드 : 같은 부모 노드의 자식들

5. 조상 노드 : 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들

6. 서브트리 : 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리

7. 자손 노드 : 서브트리에 있는 하위 레벨의 노드들

8. **차수**
    
    8-1. 노드의 차수 : 노드에 연결된 자식 노드의 수
    
    8-2. 트리의 차수 : 트리에 있는 노드의 차수 중에서 가장 큰 값
    
    8-3. 단말 노드(리프 노드): 차수가 0인 노드. 자식 노드가 없는 노드
    
9. 높이
    
    9-1. 노드의 높이 : 루트에서 노드에 이르는 간선의 수. 노드의 레벨
    
    9-2. 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-1.png)

</div>
</details>

### "이진 트리(Binary Tree)"

`: 모든 노드들이 2개의 서브트리를 갖는 형태의 트리`

- 각 노드가 자식 노드를 최대 2개까지만 가질 수 있는 트리

    - left child node

    - right child node

```
[주의]

- ! 레벨 i에서 노드의 최대 개수는 2**i 개

- ! 높이가 h인 이진 트리가 가질 수 있는 노드의 최소 개수는 (h + 1) 개가 되며, 최대 개수는(2**(h + 1) - 1) 개가 된다.
```

#### 완전 이진 트리

- 모든 레벨에서 왼쪽부터 오른쪽으로 노드가 모두 채워진 트리

- **마지막 레벨을 제외하고는 항상 완전히 채워진 상태를 유지한다.**

- 각 노드가 최대 두 개의 자식 노드를 갖는다.

- 노드의 개수는 최소 2^ ~ (2^(h + 1) - 1)

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-5.png)

#### 포화 이진 트리

- 모든 레벨에 노드가 포화상태로 차 있는 이진 트리

- 높이가 h일 떄, 최대의 노드 개수를 가지는 이진 트리

- 루트를 1번으로 하여 마지막 노드(2**(h + 1) - 1)까지 정해진 위치에 대한 노드번호를 가진다.

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-6.png)

#### 편향 이진 트리(skewed binary tree)

- 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가지는 이진트리

    - 왼쪽 편향 이진 트리

    - 오른쪽 편향 이진 트리

        ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-7.png)

<br>

## 트리 순회

`: 트리의 각 노드를 중복되지 않게 전부 방문하는 것`

### 1. 전위 순회(pre-order)

`: 부모노드 방문 후, 자식 노드를 좌, 우 순서로 방문`

- 수행 방법

    1. 현재 노드 n을 방문하여 처리(V)

    2. 현재 노드 n의 왼쪽 서브 트리로 이동(L)

    3. 현재 노드 n의 오른쪽 서브 트리로 이동(R)

    ```py
    # 재귀로 진행
    def preorder_traverse(T):
    if T:
        visit(T)        # print(T.item)
        preorder_traverse(T.left)
        preorder_traverse(T.right)
    ```

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-2.png)


### 2. 중위 순회(in-order)

`: 왼쪽 자식노드, 부모노드, 오른쪽 자식노드 순으로 방문`

- 수행 방법

    1. 현재 노드 n의 왼쪽 서브 트리로 이동(L)

    2. 현재 노드를 방문하여 처리(V)

    3. 현재 노드 n 의 오른쪽 서브 트리로 이동(R)

    ```py
    # 재귀로 진행
    def inorder_traverse(T):
    if T:
        inorder_traverse(T.left)
        visit(T)        # print(T.item)
        inorder_traverse(T.right)
    ```

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-3.png)


### 3. 후위 순회(post-order)

`: 자식 노드를 좌.우 순서로 방문한 후 부모노드를 방문`

- 수행 방법

    1. 현재 노드 n의 왼쪽 서브트리로 이동(L)

    2. 현재 노드 n 의 오른쪽 서브트리로 이동(R)

    3. 현재 노드를 방문하여 처리(V)

    ```py
    def postorder_traverse(T):
    if T:
        postorder_traverse(T.left)
        postorder_traverse(T.right)
        visit(T)        # print(T.item)
    ```

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-4.png)



### 4. 레벨 순회(level-order)

`: 노드의 레벨 순서대로 순회. 레벨이 같을 경우 왼쪽 -> 오른쪽 순서로 순회`

- bfs와 같은 동작을 수행한다.

- 수행 방법

    1. 첫 번째 레벨의 노드들을 방문한다.

    2. 두 번째 레벨의 노드들을 방문한다.

        ...
    
    3. N번째 레벨의 노드들을 방문한다.

    ```py
    from collections import deque

    def levelorder_treaverse(ST):
        queue = deque([ST])
        while queue:
            T = queue.popleft()
            print(T)
            queue.append(T.left)
            queue.append(T.right)
    ```

<br>

## 이진 탐색 트리

- 탐색 작업을 효율적으로 하기 위한 자료구조

- 모든 원소는 서로 다른 유일한 키를 갖는다.

- key(왼쪽 서브 트리) < key(루트 노드) < key(오른쪽 서브 트리)

- 서브 트리 모두 이진 탐색 트리로 표현된다.

- 중위 순회 시 오름차순의 값을 얻을 수 있음

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-8.png)

### 탐색 연산

1. 루트에서 시작한다.

2. 탐색할 키 값 x를 루트 노드의 키 값과 비교한다.

    - (x = 루트노드의 키 값)인 경우 : 원하는 원소를 찾았으므로 탐색 연산 성공

    - (x < 루트노드의 키 값)인 경우 : 루트노드의 왼쪽 서브트리에 대해 탐색연산 수행

    - (x > 루트노드의 키 값)인 경우 : 루트노드의 오른쪽 서브트리에 대해 탐색연산 수행

3. 서브트리에 대해서 순환적으로 탐색 연산을 반복한다.

### 삽입 연산

1. 먼저 탐색 연산을 수행

    - 삽입할 원소와 같은 원소가 트리에 있으면 삽입 불가능. -> 같은 원소가 있는지 탐색을 우선 진행

    - 탐색에서 탐색 실패가 결정되는 위치가 삽입 위치가 된다.

2. 탐색 실패한 위치에 원소를 삽입

    ![Alt text](/resources/Computer%20Science/Data%20Structure/Tree/image-9.png)

- 특징

    - 탐색, 삽입, 삭제 시간은 트리의 높이 만큼 시간이 걸린다.

        - $O(h)$, h : BST의 깊이

    - 평균의 경우

        - 이진 트리가 균형적으로 생성되어 있는 경우 : $O(logn)$

    - 최악의 경우

        - 한쪽으로 치우친 경사 이진 트리의 경우 : $O(n)$

        - 순차 탐색과 시간복잡도가 같다.

### 삭제 연산

1. 원소 탐색 후 값을 비교하여 서브트리를 끌어올려준다.

<br>

#### [참고 자료]

- [링크](https://www.geeksforgeeks.org/binary-tree-data-structure/)
