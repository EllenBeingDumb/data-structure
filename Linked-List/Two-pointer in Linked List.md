# Two-pointer in Linked List
> come from leetcode 
## Problem 1 - Linked list cycle
`To determine whether a linked list has cycle in it`

We use two pointers - one is slower and one is faster. If the list has a cycle, the two pointers will meet eventually. 

Here is the code I wrote: 
```
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if head is None or head.next is None:
            return False
        slow = head.next
        fast = head.next.next 
        while True:
            if slow==fast:
                return True
            if slow and slow.next and fast and fast.next:
                slow = slow.next
                fast = fast.next.next
            else:
                return False
```
## Problem 2 - Intersection of two Linked list
`idea of solution` I only think of the brute Force solution, I check the solution provided by leetcode which use the two pointers method:
1. Maintain two pointers pApA and pBpB initialized at the head of A and B, respectively. Then let them both traverse through the lists, one node at a time.
2. When pApA reaches the end of a list, then redirect it to the head of B (yes, B, that's right.); similarly when pBpB reaches the end of a list, redirect it the head of A.
3. If at any point pApA meets pBpB, then pApA/pBpB is the intersection node.
4. The last nodes must be the same if the two list have intersection. 

Here is my code:
```
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        pA,a = headA,headA
        pB,b = headB,headB
        if headA is None or headB is None:
            return None
        while True:
            if a is None or a.next is None:
                lastA = a
                break
            a = a.next
        while True:
            if b is None or b.next is None:
                lastB = b
                break
            b = b.next
        if lastA != lastB:
            return None 
        
        while True: 
            if pA == pB:
                return pA
            pA = headB if pA is None or pA.next is None else pA.next 
            pB = headA if pB is None or pB.next is None else pB.next
            
```

            
