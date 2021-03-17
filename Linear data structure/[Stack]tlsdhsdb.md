# 🧡 **STACK** 



## **What is Stack ?** 🤔

마지막에 들어온 것이 먼저 나가는 LIFO(Last In First Out) 구조를 가진 자료구조. 대표적인 예가 브라우저의 뒤로가기.

![image-20210317150043473](C:\Users\ADMIN.DESKTOP-BIOGEDJ\AppData\Roaming\Typora\typora-user-images\image-20210317150043473.png)



## **What is Queue ?** 🤔

스택과 달리 선입선출(FIFO) 구조를 가지고 있다. 대표적인 예로는 대기번호가 있다.

![image-20210317150322853](C:\Users\ADMIN.DESKTOP-BIOGEDJ\AppData\Roaming\Typora\typora-user-images\image-20210317150322853.png)

은행 번호표의 경우를 생각해보자, 번호표 시스템 내부에서는 `다음 서비스를 받을 번호` 와 `가장 나중에 온 손님이 번호표를 뽑았을 때 몇 번의 번호표를 주어야할지` 를 어떻게 기억할까? 이러한 것을 편리하게 저장하려면 `서비스를 받을 처음 위치` `서비스를 받는 마지막 위치` 두개만 기억하면 된다. 이러한 위치를 큐에서는 `front` `rear` 이라고 한다.

##  

## **Valid Parentheses**

### [Problem Link](https://leetcode.com/problems/valid-parentheses/submissions/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

 

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```

**Example 4:**

```
Input: s = "([)]"
Output: false
```

**Example 5:**

```
Input: s = "{[]}"
Output: true
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

##### **CODE**

``` python
class Solution:
    def isValid(self, s: str) -> bool:
        table = {
           "]":"[",
           "}":"{",
           ")":"("
        }
        stack = []
        
        for val in s :
            if val not in table:
                stack.append(val)
            elif not stack or table[val] != stack.pop() :
                return False
        return len(stack) == 0
```

![image-20210317143905308](C:\Users\ADMIN.DESKTOP-BIOGEDJ\AppData\Roaming\Typora\typora-user-images\image-20210317143905308.png)



## **Implement Stack using Queues**

[Problem Link](https://leetcode.com/problems/implement-stack-using-queues/)

Implement a last in first out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal queue (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

- `void push(int x)` Pushes element x to the top of the stack.
- `int pop()` Removes the element on the top of the stack and returns it.
- `int top()` Returns the element on the top of the stack.
- `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a queue, which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue), as long as you use only a queue's standard operations.

 

**Example 1:**

```
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
```

 

**Constraints:**

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
- All the calls to `pop` and `top` are valid.

 

**Follow-up:** Can you implement the stack such that each operation is **[amortized](https://en.wikipedia.org/wiki/Amortized_analysis)** `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer. You can use more than two queues.



**CODE**

```python
class MyStack:

    def __init__(self):
        self.inqueue = []
        self.dequeue = []
        

    def push(self, x: int) -> None:
        self.inqueue.append(x)

    def pop(self) -> int:
        if self.dequeue is [] and len(self.inqueue) > 1 :
            self.dequeue.append(self.inqueue.pop())
            return self.inqueue.pop()
        elif self.inqueue :
            return self.inqueue.pop()
        

    def top(self) -> int:
        if self.inqueue and self.dequeue == [] :
                return self.inqueue[-1]
        elif len(self.inqueue) == 1 and len(self.dequeue) == 1 :
                return self.dequeue[-1]        

    def empty(self) -> bool:
        return len(self.inqueue) == 0 and len(self.dequeue) == 0
        


# Your MyStack object will be instantiated and called as such:
obj = MyStack()
obj.push(2)
param_2 = obj.pop()
param_3 = obj.top()
param_4 = obj.empty()

```

스택 두개를 이용한 풀이 

[reference](https://plas.tistory.com/126)



![image-20210317155145829](C:\Users\ADMIN.DESKTOP-BIOGEDJ\AppData\Roaming\Typora\typora-user-images\image-20210317155145829.png)