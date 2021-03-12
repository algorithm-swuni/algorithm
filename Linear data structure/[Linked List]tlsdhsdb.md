# Swap Nodes in Pairs

https://leetcode.com/problems/swap-nodes-in-pairs/

```python
class Solution: 
    def swapPairs(self, head: ListNode) -> ListNode:
        def swapNode(isHead,head,newHead):
            if head and head.next :
                if isHead is False:
                    isHead = True
                    newHead = head
                temp = head.val 
                head.val = head.next.val
                head.next.val = temp
            
                if head.next.next is not None :
                    return (swapNode(isHead,head.next.next,newHead))
                else :
                    return newHead
            else :
                return head
 
        
        newHead = ListNode()
        answer = swapNode(False,head,newHead)
        return answer
```

기본 케이스는 충족하지만 홀수일 경우를 고려하지 못함.

무언가, 재귀구조를 이용하려했으나 실패함.

```python
class Solution: 
    def swapPairs(self, head: ListNode) -> ListNode:
        root = prev = ListNode(None)
        prev.next = head
        while head and head.next :
            b = head.next
            head.next = b.next
            b.next = head
            
            prev.next = b
            
            head = head.next
            prev = prev.next.next
            
        return root.next
```

단순하게 바꾸고 넘어가는 구조

![image-20210312214100146](https://user-images.githubusercontent.com/42714724/110946098-d3101b00-8381-11eb-822c-aee1d014a5bc.png)






# Add Two Numbers

https://leetcode.com/problems/add-two-numbers/

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        root = prev = ListNode(None)

        num1 = ''
        num2 = ''
        
        while l1 :
            num1 = num1+str(l1.val)
            l1 = l1.next
        while l2 :
            num2 = num2+str(l2.val)
            l2 = l2.next
            
        hap = int(num1[::-1])+int(num2[::-1])
        hap = (str(hap)[::-1])
    
        
        for h in hap :
            prev.next = ListNode(int(h),None)
            prev = prev.next
        return root.next
```

앞에서 이용한 노드의 구조와 자료형을 변환하는 것을 합침.
![image-20210312221449507](https://user-images.githubusercontent.com/42714724/110946133-da372900-8381-11eb-92a0-ec4a6b697c00.png)
