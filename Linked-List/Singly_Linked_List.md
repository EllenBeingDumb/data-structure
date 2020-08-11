# Singly Linked List
### Basic information:
Each node in a singly-linked list contains not only the value but also a reference field to link to the next node. By this way, the singly-linked list organizes all the nodes in a sequence.

### The code I wrote to design a singly linked list:
```
class Node:
    // node object
    def __init__(self,val):
        self.val=val
        self.next = None
        
class MyLinkedList:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.head = Node(None)
        self.size = 0
        
    def get(self, index: int) -> int:
        """
        Get the value of the index-th node in the linked list. If the index is invalid, return -1.
        """
        if index >= self.size:
            return -1
        if index ==0:
            return self.head.val
        cur = self.head
        for i in range(1,index+1):
            cur = cur.next
        return cur.val
            
    def addAtHead(self, val: int) -> None:
        """
        Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
        """
        new = Node(val)
        if self.size == 0:
            self.head=new
        else:
            last_new = self.head
            new.next = last_new
            self.head = new
        self.size+=1

    

    def addAtTail(self, val: int) -> None:
        """
        Append a node of value val to the last element of the linked list.
        """
        new = Node(val)
        if self.size == 0:
            self.head = new
        elif self.size ==1:
            self.head.next = new
        else:
            last = self.head
            for i in range(1,self.size):
                last = last.next
            last.next = new
        self.size+=1
        
    def addAtIndex(self, index: int, val: int) -> None:
        """
        Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
        """
        add = Node(val)
        if index == 0:
            self.addAtHead(val)
        elif index == self.size:
            self.addAtTail(val)
       
        elif index < self.size:
            cur = self.head
            for i in range(1,index+1):
                cur = cur.next
            add.next = cur
            if index ==1:
                pre = self.head
            else:
                pre = self.head
                for i in range(1,index):
                    pre = pre.next
            pre.next = add
            self.size+=1
        else:
            return 
            
    def deleteAtIndex(self, index: int) -> None:
        """
        Delete the index-th node in the linked list, if the index is valid.
        """
        if index ==0:
            head = self.head.next
            self.head = head
        elif index == self.size-1:
            if self.size == 2:
                self.head.next =None
            else:
                last = self.head
                for i in range(1,index):
                    last = last.next
                last.next = None
        elif index < self.size-1:
            pre = self.head
            if index==1:
                pre =self.head
            else:
                for i in range(1,index):
                    pre = pre.next
            nex = pre.next.next
            pre.next = nex
        
        else:
            return 
        
        self.size-=1
```
### Problem 1 - reverse linked list
>come from leetcode

*The idea is that gradually move each one after the head to the start.*

For example: a list is \[1,2,3,4,5]

it becomes: \[2,1,3,4,5]\> \[3,2,1,4,5] \> \[4,3,2,1,5] \> \[5,4,3,2,1]

```
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        p = head
        if p is None or p.next is None:
            return head
        while p.next is not None:
            cur = p.next
            p.next = cur.next
            cur.next = head
            head = cur
        return head 
```
### Remove Linked List Elements
> from leetcode

*remove all nodes that have value val*

For example:

\[1,2,3,4,5,6] remove 6 \> \[1,2,3,4,5]

Here is my solution:
```
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        
        # solve the case [val,val,val...a,b,c,d]
        while head is not None and head.val == val :
            head = head.next
        
        #solve the case [] or [n] 
        #the order matters since [] can happen after action 1
        p = head
        if p is None or (p.next is None and p.val !=val):
            return head
            
        #solve the general case[a,b,c,d,val,s,f,g]
        while True:
            if p and p.next:
                # in case there are successive dupilcates in the middle like [1,2,3,3,3,3,3,4,5]
                while p.next.val == val:
                    p.next = p.next.next
                    if p.next is None:
                         break
            if p.next is None:
                break
            p = p.next
        return head
```
#### Dummy head
