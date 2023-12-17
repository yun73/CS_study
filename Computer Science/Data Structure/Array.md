### 배열 (Array)

- 가장 기본적인 순차적인(sequential) 자료구조
- 자료들간의 관계가 1:1 선형 관계를 가진다

#### 특징
- 배열 기반으로 구현되어 연속되는 메모리 공간에 저장되는 리스트
- 인덱스 번호를 이용해서 매우 빠르게 접근할 수 있다.
- 메모리 공간으로 연속적으로 배정받기 때문에 메모리 공간 사용 효율이 좋다.
- 삽입/삭제 연산 과정에서 연속되는 메모리 배열을 위해 원소들의 이동이 필요하기 때문에 작업이 번거롭다.
- 원소의 개수가 많고 삽입/삭제 연산이 빈번하게 일어날수록 작업에 소요되는 시간이 크게 증가한다.

#### C 언어의 배열
```C
// C언어 에서의 배열
int  A[4] = {2,4,0,5};
```
- 정수는 4byte 씩 차지함

> A[2] = A[2] + 1 ___ 왼쪽의 과정에서 <br>
> 쓰기 대입 읽기 산술 ___ 연산이 발생함
> 어떻게 읽기와 쓰기가 1, 즉 상수 시간내에 가능한가?

- A[2] 의 주소 : RAM > 주소만 있다면 단일 시간 내에 값을 가져올 수 있음

> A[2] = A[0] 의 주소 + 2 * 4bytes <br>
> A[0] = 100 이라면 A[2] = 108 번 주소에 존제
> 즉 배열의 인덱스를 통해 가능


<br/>

#### Python 의 배열

- list(리스트)


```python
A = [2,4,0,5]
```
- 위의 리스트 안의 값들은 객체로 이미 메모리 상에 존재
- 즉, A[0] 은 2 라는 값(원소)을 나타내는게 아니라 해당 값이 저장된 주소를 가리킴

> 그럼 C 언어에서 A[2] = A[2] + 1 이 과정을 똑같이 한다면? <br>
> A[2] 의 값인 0을 더이상 가르키지 않고 1 이라는 새로운 주소를 가르킨다

##### 파이썬의 기본 연산 참고
```python
A.append(6) # 맨 뒤에 6을 삽입
A.pop() # 맨뒤에 값을 지우고 리턴
A.pop(1) # A[1]을 제거하고 리턴
# 빈 곳을 채우면서 땡겨짐 A[1] 4를 가르키다 0 을 가르킴
A.insert(1,10) # A[1] 에 10을 삽입
A.remove(value) # A 에서 value 값을 찾아서 cjtqjsWo rkqt wprj
A.index(value)
A.count(value)
```

#### 차이점

##### 기능
> C 언어에서는 **읽기**와 **쓰기**만 가능하지만
> 파이썬에서는 매우 다양한 기능 제공함
> C 언어에서 사용시 함수를 만들어 기능을 구현해야함

##### 용량
- list : 용량 자동조절(dynamic array)

```python
import sys
A = [] # 빈 리스트
print(sys.getsizeof(A)) # 28bytes
A.append(10) # A = [10]
print(sys.getsizeof(A)) # 44 bytes
```

![리스트 클래스](/resources/list.png)
> 리스트 클래스는 다음과 같은 속성을 가지고 있음

```python
# A.append(x) 의 내부 과정
A = []

if A.n < A.capacity:
    A[n] = x
    A.n = n + 1
elif A.n == A.capacity:
    B = A.capacity*2 # 용량이 더 큰 리스트 새로 할당

    # O(N) 의 복사 과정
    for i in range(n):
        B[i] = A[i]
    
    del A
    A = B
    # 용량 증가했으므로 n의 위치에 x 값 저장 가능
    A[n] = x
    A.n = n+1
```

> C 언어에서는 malloc 등을 이용해야함


<br/>

1. #### 배열 회전 프로그램



![img](https://t1.daumcdn.net/cfile/tistory/99AFA23F5BE8F31B0C)


<br/>

- [기본적인 회전 알고리즘 구현]()

  > temp를 활용해서 첫번째 인덱스 값을 저장 후
  > arr[0]~arr[n-1]을 각각 arr[1]~arr[n]의 값을 주고, arr[n]에 temp를 넣어준다.
  >
  > ```python 
  > def leftRotatebyOne(arr, int n):
  >     temp = arr[0]
  >     for i in range(n)
  >         arr[i] = arr[i+1]
  >     arr[n] = temp
  > ```
  >
  > 이 함수를 활용해 원하는 회전 수 만큼 for문을 돌려 구현이 가능

  <br/>

- [저글링 알고리즘 구현]()

> ![ArrayRotation](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/arra.jpg)
>
> 최대공약수 gcd를 이용해 집합을 나누어 여러 요소를 한꺼번에 이동시키는 것
>
> 위 그림처럼 배열이 아래와 같다면
>
> arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}
>
> 1,2,3을 뒤로 옮길 때, 인덱스를 3개씩 묶고 회전시키는 방법이다.
>
> a) arr [] -> { **4** 2 3 **7** 5 6 **10** 8 9 **1** 11 12}
>
> b) arr [] -> {4 **5** 3 7 **8** 6 10 **11** 9 1 **2** 12}
>
> c) arr [] -> {4 5 **6**  7 8 **9** 10 11 **12** 1 2 **3** }
> 
>```python
>def gcd(a,b):
>    if b == 0:
>        return a
>    
>    else:
>        return gcd(b,a%b)
>```
>

  <br/>

- [역전 알고리즘 구현]()

  > 회전시키는 수에 대해 구간을 나누어 reverse로 구현하는 방법
  >
  > d = 2이면
  >
  > 1,2 / 3,4,5,6,7로 구간을 나눈다.
  >
  > 첫번째 구간 reverse -> 2,1
  >
  > 두번째 구간 reverse -> 7,6,5,4,3
  >
  > 합치기 -> 2,1,7,6,5,4,3
  >
  > 합친 배열을 reverse -> **3,4,5,6,7,1,2**
  >
  >
  >
  > - swap을 통한 reverse
  >
  > ```python
  > def reverseArr(arr, int start, int end):
  >     
  >     while (start < end)
  >         temp = arr[start]
  >         arr[start] = arr[end]
  >         arr[end] = temp
  >         
  >         start += 1
  >         end -= 1
  > ```
  >
  >
  >
  > - 구간을 d로 나누었을 때 역전 알고리즘 구현
  >
  > ```python
  > def rotateLeft(arr, int d, int n):
  >     reverseArr(arr, 0, d-1)
  >     reverseArr(arr, d, n-1)
  >     reverseArr(arr, 0, n-1)
  > 
  > ```

<br/>

<br/>

2. #### 배열의 특정 최대 합 구하기


**예시)** arr[i]가 있을 때, i*arr[i]의 Sum이 가장 클 때 그 값을 출력하기 

(회전하면서 최대값을 찾아야한다.)

```
Input: arr = [1, 20, 2, 10]
Output: 72

2번 회전했을 때 아래와 같이 최대값이 나오게 된다.
{2, 10, 1, 20}
20*3 + 1*2 + 10*1 + 2*0 = 72

Input: arr= [10, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Output: 330

9번 회전했을 때 아래와 같이 최대값이 나오게 된다.
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
0*1 + 1*2 + 2*3 ... 9*10 = 330
```

<br/>

##### 접근 방법

arr[i]의 전체 합과 i*arr[i]의 전체 합을 저장할 변수 선언

최종 가장 큰 sum 값을 저장할 변수 선언

배열을 회전시키면서 i*arr[i]의 합의 값을 저장하고, 가장 큰 값을 저장해서 출력하면 된다.

<br/>

##### 해결법

```
회전 없이 i*arr[i]의 sum을 저장한 값
R0 = 0*arr[0] + 1*arr[1] +...+ (n-1)*arr[n-1]


1번 회전하고 i*arr[i]의 sum을 저장한 값
R1 = 0*arr[n-1] + 1*arr[0] +...+ (n-1)*arr[n-2]

이 두개를 빼면?
R1 - R0 = arr[0] + arr[1] + ... + arr[n-2] - (n-1)*arr[n-1]

2번 회전하고 i*arr[i]의 sum을 저장한 값
R2 = 0*arr[n-2] + 1*arr[n-1] +...+ (n?1)*arr[n-3]

1번 회전한 값과 빼면?
R2 - R1 = arr[0] + arr[1] + ... + arr[n-3] - (n-1)*arr[n-2] + arr[n-1]


여기서 규칙을 찾을 수 있음.

Rj - Rj-1 = arrSum - n * arr[n-j]

이를 활용해서 몇번 회전했을 때 최대값이 나오는 지 구할 수 있다.
```

[구현 소스 코드 링크](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/code/maxvalue_array.cpp)

<br/>

<br/>

3. #### 특정 배열을 arr[i] = i로 재배열 하기

**예시)** 주어진 배열에서 arr[i] = i이 가능한 것만 재배열 시키기

```
Input : arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1}
Output : [-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]

Input : arr = {19, 7, 0, 3, 18, 15, 12, 6, 1, 8,
              11, 10, 9, 5, 13, 16, 2, 14, 17, 4}
Output : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 
         11, 12, 13, 14, 15, 16, 17, 18, 19]
```

arr[i] = i가 없으면 -1로 채운다.



##### 접근 방법

arr[i]가 -1이 아니고, arr[i]이 i가 아닐 때가 우선 조건

해당 arr[i] 값을 저장(x)해두고, 이 값이 x일 때 arr[x]를 탐색

arr[x] 값을 저장(y)해두고, arr[x]가 -1이 아니면서 arr[x]가 x가 아닌 동안을 탐색

arr[x]를 x값으로 저장해주고, 기존의 x를 y로 수정

```
int fix(int A[], int len){
    
    for(int i = 0; i < len; i++) {
        
        
        if (A[i] != -1 && A[i] != i){ // A[i]가 -1이 아니고, i도 아닐 때
            
            int x = A[i]; // 해당 값을 x에 저장
            
            while(A[x] != -1 && A[x] != x){ // A[x]가 -1이 아니고, x도 아닐 때
                
                int y = A[x]; // 해당 값을 y에 저장
                A[x] = x; 
                
                x = y;
            }
            
            A[x] = x;
            
            if (A[i] != i){
                A[i] = -1;
            }
        }
    }
    
}
```

[구현 소스 코드 링크](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/code/rearrange_array.cpp)

<br/>
