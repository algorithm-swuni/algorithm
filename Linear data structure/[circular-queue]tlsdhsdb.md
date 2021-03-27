# 원형 큐

참고자료: https://lktprogrammer.tistory.com/59
태그: Queue, 선형자료구조

# 원형 큐

선형큐의 문제점을 보완하기 위한 자료구조이다. 선형큐의 문제점은 rear이 가르키는 포인터가 배열의 마지막 인덱스를 가르키고 있을 떄 앞쪽에서 디큐로 발생한 배열의 빈 공간을 활용 할 수 없다는 것이었는데. 원형큐에서는 포인터 증가 방식이 사이즈에 맞추어 변환되기 때문에 배열의 첫 인덱스부터 다시 데이터의 삽입이 가능해집니다.

초기화 상태

![Untitled](https://user-images.githubusercontent.com/42714724/112713627-8f88e580-8f19-11eb-97f3-12610c9a5155.png)



## Enqueue

- rear의 포인터를 1증가 시키고 그 위치에 데이터 삽입이 이루어진다.
- 만약 rear+1이 배열의 끝이고 포화상태가 아니라면 배열의 첫번째 인덱스에 데이터를 삽입한다. 배열의 포화상태 여부를 판단하기 위해 배열의 1칸은 비워둔다.
- (rear+1)%arraysize == front 라면 배열이 포화상태인걸로 판단하여 데이터 삽입이 이루어지지 않게된다.

## Dequeue

- front의 포인터를 1 증가 시키고 그 위치의 데이터를 배열에서 가지고 옵니다. rear == front 조건이라면 배열이 공백 상태인걸로 판단하여 Dequeue가 실행되지 않습니다.

# 원형큐 디자인

[https://leetcode.com/problems/design-circular-queue/](https://leetcode.com/problems/design-circular-queue/)

원형 큐의 구현을 설계합니다. 

원형 큐는 FIFO(First In First Out) 원칙에 따라 연산이 수행되고,

마지막 위치가 원을 만들기 위해 첫 번째 위치로 다시 연결되는 선형 데이터 구조입니다. 

그것은 또한 "링 버퍼"라고도 불리는데 , 원형 큐의 장점 중 하나는 큐 앞의 공간을 활용할 수 있다는 것 이다. 일반 대기열에서는 일단 대기열이 가득 차면 대기열 앞에 공백이 있더라도 다음 요소를 삽입할 수 없다. 그러나 원형 큐를 사용하면 공간을 사용하여 새 값을 저장할 수 있습니다.

- `MyCircularQueue(k)` 큐 크기를 k로 하여 개체를 초기화합니다.
- `int Front()` 대기열에서 전면 항목을 가져옵니다. 대기열이 비어 있으면 -1을 반환합니다.
- `int Rear()` 대기열에서 마지막 항목을 가져옵니다. 대기열이 비어 있으면 -1을 반환합니다.
- `boolean enQue(int value)` 요소를 원형 큐에 삽입합니다. 작업이 성공하면 true를 반환합니다.
- `boolean deQueue()` 원형 대기열에서 요소를 삭제합니다. 작업이 성공하면 true를 반환합니다.
- `boolean isEmpty()` 원형 대기열이 비어 있는지 여부를 확인합니다. boolean is Full() 원형 큐가 가득 찼는지 여부를 확인합니다.
- `boolean isFull()` 원형 대기열이 가득 차 있는지 여부를 확인합니다.

```python
class MyCircularQueue:

    def __init__(self, k: int):
        self.q = [None] * k  ## k 만큼의 빈 공간을 확보한 빈 큐를 만든다.
        self.front = 0 ## front 포인터를 초기화 합니다.
        self.rear = 0 ## rear 포인터를 초기화 합니다.
        self.maxlen = k ## mod 연산에 필요한 큐의 길이 정보를 저장합니다.
        
    def enQueue(self, value: int) -> bool:
        #value 값을 넣는다.
        if self.q[self.rear] is None : 
            # rear 가 가리키는 자리가 비어 있지 않다면 (rear가 가리키는 자리는 항상 None이어야 한다, 한자리를 남겨 놓아야 하기 때문) False 를 리턴한다 . 큐가 꽉차있거나 비정상적인 상태이기 때문이다.
            self.q[self.rear] = value # 큐의 rear 자리에 value 값을 넣습니다.
            self.rear = (self.rear + 1) % self.maxlen ## 원형 큐이기 때문에 mod 연산을 이용한다.
            return True
        else :
            return False
        
    def deQueue(self) -> bool:
        if self.q[self.front] is None :
            # 인큐의 경우와는 다르게 front가 가리키는 값이 없다면 공백큐이거나 비정상적이라는 상황이기 때문에 False 를 리턴한다.
            return False 
        else :
            self.q[self.front] = None # front 자리에 None을 할당한다. 아무값도 없다는것을 알려주어야한다. 다른값이 들어와도 된다는 일종의 시그널같은 것 
            self.front = (self.front + 1) % self.maxlen # 원형큐이기 때문에 가리키는 부분에 대한 mod 연산을 한다.
            return True

    def Front(self) -> int:
        # front 가 가리키는 값이 None이면 값이 없기 때문에 -1 를 리턴하고 값이 존재하면 front가 가리키는 값을 리턴
        return -1 if self.q[self.front] is None else self.q[self.front]

    def Rear(self) -> int:
        # rear 값이 현재 가리키는 값은 항상 비어있다 그렇기 때문에 가장 끝에 있는 값을 리턴하기 위해 -1한 값을 리턴
        return -1 if self.q[self.rear-1] is None else self.q[self.rear-1]

    def isEmpty(self) -> bool:
        # front 가 가리키는 값과 rear가 가리키는 값이 같고 front 가 가리키는 값도 None이어야 한다.
        return self.front == self.rear and self.q[self.front] is None
        

    def isFull(self) -> bool:
        return self.front == self.rear and self.q[self.front] is not None
```

![Untitled 1](https://user-images.githubusercontent.com/42714724/112713636-99124d80-8f19-11eb-9459-1b889e734ab4.png)


### isEmpty / isFull ?

처음에는 단순하게 비어있는 경우 rear와 front의 포인터가 일치하면 되지 않나? 라고 생각을 했고 해당 케이스에 대한 의문을 풀어줄 테스트 케이스를 가지고 생각해보려고 한다.

["MyCircularQueue","enQueue","Front","isFull","enQueue","enQueue","enQueue","deQueue","enQueue","enQueue","isEmpty","Rear"]

[[4],[3],[],[],[7],[2],[5],[],[4],[2],[],[]]

해당 케이스에 대한 정답은 다음과 같다 :
[null,true,3,false,true,true,true,true,true,false,false,4]

isEmpty 마지막에서 두번째 명령인데 해당 명령에서 확인하고 싶은 내용은 full인 상태에서 isEmpty 를 입력함으로서 empty와 full을 명확하게 구분하고 있는지를 확인하기 위해서이다.

두 포인터가 같은 것은 비어있음과 가득참을 구분하는 척도가 될 수 없기 때문에 명확하게 해야하는데 비어있는 상태는 두 포인터가 가리키는 곳에 None이 할당되어있을 것이고 가득찬 상태일 경우 두 포인터가 가리키는 곳은 None이 아니고 다른 값이 있을 것 이다. 

이러한 경우의 수를 고려해주어야 한다.
