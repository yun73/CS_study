## 트라이(Trie)
트라이(Trie)는 문자열을 저장하고 효율적으로 탐색하기 위한 **트리 형태**의 자료구조이다.

우리가 검색할 때 볼 수 있는 **자동완성 기능, 사전 검색** 등 **문자열을 탐색하는데 특화되어있는 자료구조**라고 한다.

만약 Datastructure라는 단어를 검색하기 위해서는 제일 먼저 'D'를 찾고, 다음에는 'a', 't'순서로 찾아가는 개념을 **트라이(trie)** 라고 한다.

<br>

### 트라이 장단점
트라이는 문자열 검색을 빠르게 한다.

문자열을 탐색할 때, 하나 하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 효율적이다.

각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다는 단점이 있다.(메모리 측면에서 비효율적일 수 있음)


### 트라이 이용한 문자열 삽입
![trieExample](../../resources/Computer%20Science/Data%20Structure/Trie/1.png)
<br>

<ul>'baby, ball, tree, trie' 삽입
<li> 첫 번째 문자는 'b'이다. 초기에 트라이 자료구조 내에는 아무런 자료가 없으므로 Head의 자식노드에 'b'를 추가해준다.
<li> 'b'노드에도 현재 자식이 하나도 없으므로, 'b'의 자식노드에 'a'를 추가해준다.
<li> 동일한 방식으로 'a'노드 밑에 b와 l을 넣어주고,
<li> baby의 by는 b밑으로, ball의 bl은 l밑으로 넣어주어 트리를 완성한다.
<li> 끝으로 단어가 모두 입력되었다면 *를 넣어 언어가 끝났음을 알 수 있도록 해당 언어 다음 노드에 넣어준다.

<li>해당 순서처럼 tree와 trie를 트리에 넣어준다. </ul>

**트라이의 문자열 삽입은 O(문자열길이)**

### 트라이를 이용한 문자열 탐색

[tree 와 treem , track]을 탐색한다고 할때 

<li>tree는 t노드 -> r노드 -> e 노드 -> e 노드 -> * 를 통해 단어가 있음을 알리는 True를 반환한다.</li>
<li>treem을 탐색하는 것은 tree와 동일하게 내려가지만, m을 찾기위해 노드를 내려가보니 *가 있어 해당 문자열은 없음으로 False를 반환한다.</li>
<li>track을 찾아보면 t 노드 -> r노드 -> a 노드가 없기에 False를 반환한다.</li>

```
class Node(object):
    def __init__(self, key, data=None):
        self.key = key
        self.data = data
        self.children = {}


class Trie(object):
    def __init__(self):
        self.head = Node(None)

    # 문자열 삽입
    def insert(self, string):
        curr_node = self.head

        # 삽입할 String 각각의 문자에 대해 자식Node를 만들며 내려간다.
        for char in string:
            # 자식Node들 중 같은 문자가 없으면 Node 새로 생성
            if char not in curr_node.children:
                curr_node.children[char] = Node(char)

            # 같음 문자가 있으면 노드를 따로 생성하지 않고, 해당 노드로 이동
            curr_node = curr_node.children[char]

        # 문자열이 끝난 지점의 노드의 data값에 해당 문자열을 표시
        curr_node.data = string


    # 문자열이 존재하는지 탐색!
    def search(self, string):
        # 가장 아래에 있는 노드에서부터 탐색 시작한다.
        curr_node = self.head

        for char in string:
            if char in curr_node.children:
                curr_node = curr_node.children[char]
            else:
                return False

        # 탐색이 끝난 후에 해당 노드의 data값이 존재한다면
        # 문자가 포함되어있다는 뜻이다!
        if curr_node.data is not None:
            return True

```


---



