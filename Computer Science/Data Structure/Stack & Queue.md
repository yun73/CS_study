## 스택(Stack)



##### LIFO (Last In First Out, 후입선출) : 가장 나중에 들어온 것이 가장 먼저 나옴

<br>

***언제 사용?***


##### pop


##### isEmpty



##### isFull

#### 동적 배열 스택


#### 스택을 연결리스트로 구현해도 해결 가능



## 큐(Queue)


##### FIFO (First In First Out, 선입선출) : 가장 먼저 들어온 것이 가장 먼저 나옴

<br>

***언제 사용?***


<br>

데이터 넣음 : enQueue()

데이터 뺌 : deQueue()

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

<br>

데이터를 넣고 뺄 때 해당 값의 위치를 기억해야 함. (스택에서 스택 포인터와 같은 역할)

이 위치를 기억하고 있는 게 front와 rear

front : deQueue 할 위치 기억

rear : enQueue 할 위치 기억

<br>

##### 기본값

##### enQueue


##### deQueue


#####  isEmpty

##### isFull




**'원형 큐'**


##### 기본값


##### enQueue

<br>


##### deQueue


<br>

#####  isEmpty

<br>

##### isFull




<br>

이를 개선한 것이 '연결리스트 큐'

##### 연결리스트 큐는 크기가 제한이 없고 삽입, 삭제가 편리

<br>

##### enqueue 구현


##### dequeue 구현

