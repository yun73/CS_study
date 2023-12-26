<img src="/resources/hash_function.PNG"><br>
## 해시 함수
> 임의의 길이를 갖는 임의의 데이터를 고정된 길이의 데이터인 해시 값으로 매핑하는 함수 (역은 고려하지 않음)

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
2.  곱셈<br>
    ex) key가 200, 사용하려는 배열 크기 30<br>
        0 < a < 1 인 a 값 정하기 -> a 값에 key 곱해서 나온 값의 소수 부분만 남김 -> 남은 소수 부분에 배열 크기 곱해서 나온 값의 정수만 남김
    ```
    def hash_function_multiplication(key, array_size, a):
    temp = a \* key
    temp = temp - int(temp)
        return int(array_size * temp)
     ```

**java의 hashCode() 메서드**<br>
Object 클래스에 _hashCode()_ 메서드 있어 오버라이드하여 해시 함수 구현<br>
```java
public int hashCode() {
    return Objects.hash(att1, att2, att3)
}
```

**python의 hash 함수**<br>
파라미터로 받은 값을 _아무_ 정수로 바꿔줌<br>
서로 다른 두 값을 파라미터로 넣었을 때 같은 정수가 리턴될 수 없음(데이터를 자신만의 고유한 정수값으로 바꿔줌)<br>
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
> 무한에 가까운 데이터들을 유한의 개수 해시 값으로 매핑한 테이블.<br>

**load factor** : 해시 테이블의 한 버킷에 평균 몇 개의 키가 매핑되는가 나타내는 지표로 1보다 큰 경우 해시충돌 발생, 실제 키 개수(n)/해시테이블 크기(m)

- 해시 함수로 key를 변환한 결과값을 인덱스로 사용하여 key, value 쌍 저장
- 삽입, 삭제, 탐색 시 평균 O(1) 시간 복잡도
- unordered_map으로 구현<br>
  unorderd_map이란? C++ STL(Standard Template Library)<br>
  중복 데이터를 허용하지 않음<br>
  map이 탐색/삽입/삭제의 시간복잡도가 O(log n)인 것에 비해 더 빠른 탐색 가능 => 정렬을 보장하지 않아서<br>

하지만 데이터가 많아지면, 다른 데이터가 같은 해시 값으로 충돌나는 현상이 발생 **'collision' 현상** <br>
메모리 절약을 위해 실제 해시 함수 표현 범위(N)보다 작은 M개의 원소가 있는 배열인 "해시 버킷"만 사용<br>

**_그래도 해시 테이블을 쓰는 이유는?_**<br>
적은 리소스로 많은 데이터를 효율적으로 관리하기 위함.
인덱스에 해시값을 사용함으로써 모든 데이터 살피지 않아도 검색, 삽입, 삭제 빠르게 가능.<br>

#### 충돌 문제 해결
1. Chaining : 연결 리스트(linked list) 자료 구조를 사용
인덱스에 연결 리스트를 저장(key-value 쌍과 다음 노드에 대한 레퍼런스 저장)
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
    
2. open addressing : 충돌 발생 시 비어있는 인덱스에 값 저장, 시간복잡도 O(n), 체이닝 방식보다 캐시 효율 높음<br>
하지만 클러스터링(연속된 슬롯이 모두 채워지는 현상) 문제 발생할 수 있음 => 성능 저하

3. Bucket : 해시 테이블을 고정된 크기의 버킷으로 나누고, 각 버킷은 여러 개의 키 저장 가능<br>
클러스터링 문제 줄일 수 있으나 버킷 크기 초과하는 충돌 발생 시 성능 저하 문제<br>

**비어 있는 인덱스 찾는 방법?**
    - 선형 탐사(linear Probing)<br>
    충돌난 인덱스 바로 뒤 인덱스부터 한칸씩 확인<br>
    탐색 연산 시 빈 인덱스를 발견했다? 처음부터 그 값이 저장이 안 된 것으로 인식하고 연산 종료.<br>
    위의 이유 때문에 삭제 연산 시 빈 인덱스에 'DELETED' 또는 다른 약속된 표시 해줌<br>

    - 제곱 탐사(Quadratic Probing)<br>
    충돌난 인덱스에서 1의 제곱보다 큰 인덱스 확인 -> 그 인덱스보다 2의 제곱만큼 큰 인덱스 확인...<br>
    편차가 작은 key 값 몰려 있는 경우 효율적
    
    - 이중해싱(double hashing)<br>
    탐사할 해시값 규칙성 없애서 clustering 방지<br>
    2개의 해시 함수 준비해서 하나는 최초 해시값 얻을 때, 나머지 하나는 해시충돌 일어났을 때 탐사 이동폭 얻기 위해 사용<br>


## 해시 테이블 성능 향상법
- Consistend hasing : 해시 bit 수 늘리기 - 항목 수 적을 때 적은 bit수의 해시 사용하다 충돌 잦아지면 1bit 늘리고 저장공간도 2배 늘림 .. 점진적 확장 => 분산 데이터베이스에서 데이터 일관성 유지하기 위해 사용

## 동적 해싱(Dynamic Hashing)
- 연장 가능 해싱(Extendible Hashing)<br>
해시 테이블이 버킷(bucket)으로 나뉘며, 각 버킷은 고유의 '깊이(depth)'를 가짐. 충돌이 발생하면 해당 버킷만 분할하고, 필요한 경우 디렉토리 크기 조정.<br>
해시 테이블 각 요소(버킷)에 접근하기 위해 주로 이진 트리 구조 사용.

- 선형 해싱(Linear Hashing)<br>
점진적으로 해시 테이블 확장. 새로운 데이터 추가될 때마다 조금씩 테이블 확장하여 한 번에 발생하는 부하 분산

참고자료 : [링크](https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/)
