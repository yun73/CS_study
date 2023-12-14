## 해시 함수
> 특정 값을 원하는 범위의 자연수로 바꿔주는 함수 (역은 고려하지 않음)

- 해시 함수 조건

1. 한 해시 테이블의 해시 함수는 결정론적 (ex. 똑같은 key를 넣었을 때 항상 같은 결과가 나와야 함)
2. 결과 해시값이 치우치지 않고 고르게 나옴 (원하는 범위의 자연수 하나하나가 리턴될 확률이 최대한 비슷)
3. 연산이 빨라야 함.(효율적)<br>

- 해시 함수 만드는 법

1. 나누기 : 자연수 key를 해시테이블 크기로 나눈 나머지를 리턴

```
def hash_function_remainder(key, array_size):
    return key % array_size
```

2.  곱셈
    ex.key가 200, 사용하려는 배열 크기 30 - 0 < a < 1 인 a 값 정하기 - a 값에 key 곱하기 / 정수 버리고 소수 부분만 남김 - 남은 소수 부분에 배열 크기 곱하기 / 소수 버리고 정수만 남김
    ```
    def hash_function_multiplication(key, array_size, a):
    temp = a \* key
    temp = temp - int(temp)
        return int(array_size * temp)
        ```
    **python의 hash 함수**
    파라미터로 받은 값을 _아무_ 정수로 바꿔줌<br>
    서로 다른 두 값을 파라미터로 넣었을 때 같은 정수가 리턴될 수 없음
    (데이터를 자신만의 고유한 정수값으로 바꿔줌)<br>
    _단, 불변 타입 자료형(boolean, tuple, string 등)에만 사용_

```python
# 정수 값
print(hash(12345))  # 12345

# 소수 값
print(hash(15.1234))  # 284541027336970255

# 문자열
print(hash("파이썬"))  # -8002119629611903017
```

## 해시 테이블
> 무한에 가까운 데이터들을 유한의 개수 해시 값으로 매핑한 테이블.

- 해시 함수로 key를 변환한 결과값을 인덱스로 사용하여 key, value 쌍 저장
- 삽입, 삭제, 탐색 시 평균 O(1) 시간 복잡도
<https://programming.guide/hash-tables-complexity.html>
- unordered_map으로 구현
  unorderd_map이란? C++ STL(Standard Template Library)<br>
  중복 데이터를 허용하지 않음<br>
  map이 탐색/삽입/삭제의 시간복잡도가 O(log n)인 것에 비해 더 빠른 탐색 가능 => 정렬을 보장하지 않아서<br>

하지만 데이터가 많아지면, 다른 데이터가 같은 해시 값으로 충돌나는 현상이 발생 **'collision' 현상**

**_그래도 해시 테이블을 쓰는 이유는?_**

##### 충돌 문제 해결
- Chaining : linked list 자료 구조를 사용
인덱스에 링크드 리스트를 저장(key-value 쌍과 다음 노드에 대한 레퍼런스 저장)
```
class Node:
    """링크드 리스트의 노드 클래스"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None  # 다음 노드에 대한 레퍼런스
        self.prev = None  # 이전 노드에 대한 레퍼런스


class LinkedList:
    """필요 메서드만 가져와서 사용"""
    def __init__(self):
        self.head = None  # 링크드 리스트의 가장 앞 노드
        self.tail = None  # 링크드 리스트의 가장 뒤 노드


    # 탐색 메서드
    def find_node_with_key(self, key):
        """링크드 리스트에서 주어진 데이터를 갖고있는 노드 리턴
        단, 해당 노드가 없으면 None 리턴"""

        iterator = self.head   # 링크드 리스트를 돌기 위해 필요한 노드 변수

        while iterator is not None:
            if iterator.key == key:
                return iterator

            iterator = iterator.next

        return None


    # 추가(맨 뒤 삽입) 메서드
    def append(self, key, value):
        new_node = Node(key, value)

        # 빈 링크드 리스트라면 head와 tail을 새로 만든 노드로 지정
        if self.head is None:
            self.head = new_node
            self.tail = new_node

        # 이미 노드가 있으면
        else:
            self.tail.next = new_node  # tail의 다음 노드로 추가
            new_node.prev = self.tail
            self.tail = new_node  # tail 업데이트


    # 삭제 메서드
    def delete(self, node_to_delete):

        # 링크드 리스트에서 마지막 남은 데이터를 삭제할 때
        if node_to_delete is self.head and node_to_delete is self.tail:
            self.tail = None
            self.head = None

        # 링크드 리스트 가장 앞 데이터 삭제할 때
        elif node_to_delete is self.head:
            self.head = self.head.next
            self.head.prev = None

        # 링크드 리스트 가장 뒤 데이터 삭제할 떄
        elif node_to_delete is self.tail:
            self.tail = self.tail.prev
            self.tail.next = None

        # 두 노드 사이에 있는 데이터 삭제할 때
        else:
            node_to_delete.prev.next = node_to_delete.next
            node_to_delete.next.prev = node_to_delete.prev
```


## 해시 버킷 동적 확장

참고자료 : [링크](https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/)
