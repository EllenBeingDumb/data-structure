# Linked List
## 1. Singly Linked List
#### The code I wrote for a singly liked lis

```
class Node:
    
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
        Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked             list. If index is greater than the length, the node will not be inserted.
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

## 2. Two-pointer in linked list
#### A template 
```
// Initialize slow & fast pointers
ListNode slow = head;
ListNode fast = head;

//Change this condition to fit specific problem.
//Attention: remember to avoid null-pointer error

while (slow != null && fast != null && fast.next != null) {
    slow = slow.next;           // move slow pointer one step each time
    fast = fast.next.next;      // move fast pointer two steps each time
    if (slow == fast) {         // change this condition to fit specific problem
        return true;
    }
}
return false;   // change return value to fit specific problem
```
#### Things to be care of:
1. Always examine if the node is null before you call the next field.(null-pointer)
2. Carefully define the end conditions of your loop.(endless loop)



