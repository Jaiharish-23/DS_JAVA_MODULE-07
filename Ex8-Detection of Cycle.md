# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE:16-09-2026
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1. Start the program.

2. Create a Node class with:

data → stores the value of the node.
next → stores the reference to the next node.
Create a LinkedListCycle class with:

A method to insert elements into the linked list.
A method to create a cycle manually for testing (optional).
A method to detect a cycle using Floyd’s Cycle Detection Algorithm.
3. Cycle Detection:

Initialize two pointers, slow and fast.
Move slow one step and fast two steps at a time.
If slow and fast meet, a cycle exists.
Find the starting node of the cycle:

Reset slow to the head after the meeting point is found.
Move both slow and fast one step at a time.
The node where they meet again is the starting node of the cycle.
If no meeting point occurs, the linked list has no cycle.

4. Display the result accordingly.

5. Stop the program.   

## Program:
```
/*
program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: JAI HARISH R
RegisterNumber:  212224040124
*/
```

```java

import java.util.*;

public class Solution {

    static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
            next = null;
        }
    }

    public ListNode detectCycle(ListNode head) {
       if(head==null || head.next==null){
           return null;
       }
       ListNode slow = head;
       ListNode fast = head;
       while(fast!=null && fast.next!=null){
           slow = slow.next;
           fast = fast.next.next;
           if(slow==fast){
               ListNode entry = head;
               while(entry!=slow){
                   entry = entry.next;
                   slow = slow.next;
               }
               return entry;
           }
       }
       return null;
       
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();

        String headInput = sc.nextLine().trim().replaceAll("\\[|\\]", "");
        
        int pos = sc.nextInt();

        if (headInput.isEmpty()) {
            System.out.println("no cylce");
            return;
        }

        String[] parts = headInput.split(",");
        int[] values = Arrays.stream(parts).mapToInt(Integer::parseInt).toArray();

        ListNode head = new ListNode(values[0]);
        ListNode current = head;
        List<ListNode> nodeList = new ArrayList<>();
        nodeList.add(head);

        for (int i = 1; i < values.length; i++) {
            ListNode newNode = new ListNode(values[i]);
            current.next = newNode;
            current = newNode;
            nodeList.add(newNode);
        }

      
        if (pos >= 0 && pos < nodeList.size()) {
            current.next = nodeList.get(pos);
        }


        ListNode cycleStart = sol.detectCycle(head);

        if (cycleStart != null) {
            int index = 0;
            for (ListNode node : nodeList) {
                if (node == cycleStart) {
                    System.out.println("tail connects to node index " + index);
                    return;
                }
                index++;
            }
        } else {
            System.out.println("no cycle");
        }
    }
}

```

## Output:

<img width="995" height="217" alt="image" src="https://github.com/user-attachments/assets/27154f4c-3c51-4832-9192-57c978e73e86" />


## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.
