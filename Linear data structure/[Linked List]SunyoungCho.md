# Linked List
## Linked List 링크드 리스트
- 데이터를 순차적으로 저장하는 선형 자료구조
- 불연속적 메모리 공간
## 장점과 단점
* 장점
  - 삽입, 삭제가 용이(포인터만 변경)
  - 크기 고정(X), 동적 생성 가능
  - 메모리 재사용 가능
* 단점
  - 탐색할 때 임의 접근 불가능
  - 포인터로 인하여 저장공간 낭비
## 시간복잡도
* 삽입
  - 리스트의 맨 앞/뒤에 삽입하는 경우: O(1)
  - 리스트의 중간에 삽입하는 경우: O(n) = 탐색 시간
* 삭제
  - 리스트의 맨 앞/뒤에서 삭제하는 경우: O(1)
  - 리스트의 중간에서 삭제하는 경우: O(n) = 탐색 

## Add Two Numbers
## Problem
### You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.
### You may assume the two numbers do not contain any leading zero, except the number 0 itself.
### Example 1:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
### Example 2:
Input: l1 = [0], l2 = [0]
Output: [0]
### Example 3:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
### Constraints
- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros
### <u>Code</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        padding = 0
        result_node = ListNode()
        result_output = result_node
        while (l1 != None) or (l2 != None):
            if l1 == None:
                l1_num = 0
            else:
                l1_num = l1.val
            if l2 == None:
                l2_num = 0
            else:
                l2_num = l2.val
            # padding 없는 경우
            if padding == 0:
                add_sum = l1_num + l2_num
            else: # padding 있는 경우
                add_sum = l1_num + l2_num + padding
                padding = 0
            # padding 만드는거
            if add_sum >= 10:
                padding = add_sum // 10
                result = add_sum % 10
            else:
                result = add_sum
            result_output.next = ListNode(result)
            result_output = result_output.next
            if l1 != None:
                l1 = l1.next
            if l2 != None:
                l2 = l2.next
            # l1 = l1.next
            # l2 = l2.next
        if padding != 0:
            result_output.next = ListNode(padding)
        return result_node.next
```
### Result
![image](https://user-images.githubusercontent.com/66547492/110111328-7e095d80-7df3-11eb-9936-897bc45e2a26.png)
- While문에서 l1과 l2를 처음부터 끝까지 탐색
- 시간복잡도는 O(n)

## Swap Nodes in Paris
## Problem
### Given a linked list, swap every two adjacent nodes and return its head.
### Example 1:
Input: head = [1,2,3,4]
Output: [2,1,4,3]
### Example 2:
Input: head = []
Output: []
### Example 3:
Input: head = [1]
Output: [1]
### Constraints
- The number of nodes in the list is in the range [0, 100].
- 0 <= Node.val <= 100
### <u>Code</u>
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        node = ListNode()
        result_node = node
        
        # 데이터가 하나 또는 없는 경우
        if head == None:
            return head
        
        while head != None:
            val1 = head.val
            head = head.next
            if head != None:
                val2 = head.val
                head = head.next
            else:
                val2 = None
            if val2 != None:
                result_node.next = ListNode(val2)
                result_node = result_node.next
                result_node.next = ListNode(val1)
                result_node = result_node.next
            else:
                result_node.next = ListNode(val1)
                result_node = result_node.next
        return node.next
```
### Result
![image](https://user-images.githubusercontent.com/66547492/110111777-30412500-7df4-11eb-8d85-2a9c0ced6475.png)
- while문에서 노드를 처음부터 끝까지 탐색
- 시간복잡도는 O(n)
