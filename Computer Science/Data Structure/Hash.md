## 해시(Hash)


## 해시 테이블
- 무한에 가까운 데이터들을 유한의 개수 해시 값으로 매핑한 테이블.
- 삽입, 삭제, 탐색 시 평균 O(1) 시간 복잡도
- unordered_map으로 구현
unorderd_map이란? C++ STL(Standard Template Library)<br>
중복 데이터를 허용하지 않음<br>
map이 탐색/삽입/삭제의 시간복잡도가 O(log n)인 것에 비해 더 빠른 탐색 가능 => 정렬을 보장하지 않아서

하지만 데이터가 많아지면, 다른 데이터가 같은 해시 값으로 충돌나는 현상이 발생 **'collision' 현상**

**_그래도 해시 테이블을 쓰는 이유는?_**




##### 충돌 문제 해결


## 해시 버킷 동적 확장


참고자료 : [링크](https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/)
