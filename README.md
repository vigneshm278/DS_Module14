# Ex6 Right Rotation LinkedList
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. start the program.
2. Handle edge cases.
3. Find the length of the linked list.
4. Connect last node to head (make circular list).
5. Normalize k and find the new tail position.
6. Break the circle to form new list and return newHead.
7. Stop the program.

## Program:
```
/*
Program to  Right Rotation LinkedList
Developed by: Vignesh M
RegisterNumber:  212223240176
*/

import java.util.Scanner;
public class RotateLinkedList {
    public static Node rotate(Node head, int k) {
        if (head == null || head.next == null || k == 0) {
            return head;
        }
        Node current = head;
        int length = 1;
        while (current.next != null) {
            current = current.next;
            length++;
        }
        current.next = head;
        k = k % length;
        int stepsToNewHead = length - k;
        Node newTail = current;
        while (stepsToNewHead-- > 0) {
            newTail = newTail.next;
        }
        Node newHead = newTail.next;
        newTail.next = null;
        return newHead;
    }
    public static void display(Node head) {
        Node current = head;
        System.out.print("LinkedList: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Node head = null, tail = null;
        int n = scanner.nextInt();
        for (int i = 0; i < n; i++) {
            Node newNode = new Node(scanner.nextInt());
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        int k = scanner.nextInt();
        head = rotate(head, k);
        display(head);
        scanner.close();
    }
}
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

## Output:

<img width="899" height="243" alt="image" src="https://github.com/user-attachments/assets/b2ff88ad-e7fb-4bc8-8f91-4b4e59cf9e59" />

## Result:
Thus, the C program to perfom right rotation on linked list is implemented successfully.

# Ex7 Removal of Nodes with a Specific Value from a Linked List

## AIM:
To write a java  program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm

1. Start the program.
2. Create dummy head.
3. Set prev = dummy, curr = head.
4. Traverse list.
5. Move curr each step.
6. Return dummy.next as updated head.
7. Stop the program.
8. 
## Program:
```
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: Vignesh M
RegisterNumber:  212223240176
*/

import java.util.*;

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}

class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy, curr = head;

        while (curr != null) {
            if (curr.val == val) {
                prev.next = curr.next; 
            } else {
                prev = curr; 
            }
            curr = curr.next; 
        }

        return dummy.next; 
    }
}

public class Main {

    public static ListNode buildList(int[] arr) {
        if (arr.length == 0) return null;
        ListNode head = new ListNode(arr[0]);
        ListNode current = head;
        for (int i = 1; i < arr.length; i++) {
            current.next = new ListNode(arr[i]);
            current = current.next;
        }
        return head;
    }

    public static String listToString(ListNode head) {
        List<Integer> result = new ArrayList<>();
        while (head != null) {
            result.add(head.val);
            head = head.next;
        }
        return result.toString(); 
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        String input = scanner.nextLine().replaceAll("\\s", "");
        int[] nums = Arrays.stream(input.split(","))
                           .mapToInt(Integer::parseInt)
                           .toArray();


        int val = scanner.nextInt();
        ListNode head = buildList(nums);
        Solution solution = new Solution();
        ListNode updated = solution.removeElements(head, val);
        System.out.println(listToString(updated));

        scanner.close();
    }
}
```

## Output:

<img width="711" height="378" alt="image" src="https://github.com/user-attachments/assets/70f588ac-de12-42b9-ae1e-38a456093a03" />

## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.

# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List

## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm

1. Start the program.
2. Read input & build linked list.
3. If pos >= 0, link last node to pos node.
4. Use Floyd’s algorithm to detect cycle.
5. If no cycle → print "no cycle".
6. If cycle detected:
         Move second pointer from head until it meets slow pointer.
         That meeting point is cycle start.
7. Find index of that node in nodeList. 
8. Print "tail connects to node index X".
9. Stop the program.
   
## Program:

```
/*
program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: Vignesh M
RegisterNumber:  212223240176
*/

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
        if (head == null || head.next == null) return null;

        ListNode slow = head, fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
               
                ListNode entry = head;
                while (entry != slow) {
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

<img width="889" height="292" alt="image" src="https://github.com/user-attachments/assets/a53af8a9-f370-4bea-b8a2-baa1b53c1bdf" />

## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.

# Ex9 Finding the Longest Length of Nested Set in a Permutation Array

## AIM:
To write a program that finds the length of the longest set s[k] defined as s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … },where the iteration stops before a duplicate element occurs.

The task is to return the maximum size among all such sets.
## Algorithm

1.Start the program.
2.Input: An array nums representing a permutation of the numbers from 0 to n - 1.
3.Initialize a boolean array visited[] of size n to keep track of visited elements.
4.Initialize a variable maxLength = 0 to store the maximum length of any nested set.
5.For each index i in the array:
      i. If nums[i] is not visited:
      ii. Start from index i, and keep following nums[k] until a visited element is encountered.
      iii. Count the number of steps taken.
      iv. Update maxLength if the current count is greater than the existing value.
 6.Output the value of maxLength. End the program.

## Program:

```
/*
Program to find the Longest Length of Nested Set in a Permutation Array
Developed by: Vignesh M
RegisterNumber:  212223240176
*/

import java.util.*;
public class ArrayNestingMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine().trim();
        input = input.replace("nums =", "").replace("[", "").replace("]", "").trim();
        String[] parts = input.split(",");
        int[] nums = new int[parts.length];

        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }
        Solution sol = new Solution();
        int result = sol.arrayNesting(nums);
        System.out.println(result);
        sc.close();
    }
}
class Solution {
    public int arrayNesting(int[] nums) {
        int maxlen = 0;
        boolean[] visited = new boolean[nums.length];
        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                int count = 0;
                int curr = i;
                while (!visited[curr]) {
                    visited[curr] = true;
                    curr = nums[curr];
                    count++;
                }
                maxlen = Math.max(maxlen, count);
            }
        }
        return maxlen;

    }
}
```

## Output:

<img width="435" height="89" alt="image" src="https://github.com/user-attachments/assets/6c003441-e2bc-415f-ae4b-ec1b110ad8d6" />

## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.

# EX 10 Flattening a Nested List Using an Iterator

## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm

1. Start the program.
2. Parse string input into nested structure using stack.
3. Recursively flatten nested lists into a single list.
4. Use an iterator with pointer position to return elements sequentially.
5. Output final flattened list.
6.  Stop the program.

## Program:
```
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: Vignesh M
RegisterNumber:  212223240176
*/

import java.util.*;
public class NestedIterator implements Iterator<Integer> {
    private List<Integer> integers = new ArrayList<>();
    private int position = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flattenList(nestedList);
    }

    private void flattenList(List<NestedInteger> nestedList) {
        for (NestedInteger ni : nestedList) {
            if (ni.isInteger()) {
                integers.add(ni.getInteger());
            } else {
                flattenList(ni.getList());
            }
        }
    }

    @Override
    public Integer next() {
        if (!hasNext()) throw new NoSuchElementException();
        return integers.get(position++);
    }
    @Override
    public boolean hasNext() {
        return position < integers.size();
    }
    public static List<NestedInteger> parse(String s) {
    Stack<List<NestedInteger>> stack = new Stack<>();
    List<NestedInteger> curr = new ArrayList<>();
    int num = 0;
    boolean hasNum = false;

    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (c == '[') {
            stack.push(curr);
            curr = new ArrayList<>();
        } else if (c == ']') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
            List<NestedInteger> completed = curr;
            curr = stack.pop();
            curr.add(new SimpleNestedInteger(completed));
        } else if (c == ',') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
        } else if (Character.isDigit(c)) {
            num = num * 10 + (c - '0');
            hasNum = true;
        }
    }
    return curr;
}


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
      
        String input = sc.nextLine();

        List<NestedInteger> nestedList = parse(input);

        NestedIterator iterator = new NestedIterator(nestedList);
        List<Integer> output = new ArrayList<>();
        while (iterator.hasNext()) {
            output.add(iterator.next());
        }

        System.out.println(output);
    }
}

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class SimpleNestedInteger implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    public SimpleNestedInteger(Integer value) {
        this.value = value;
        this.list = null;
    }

    public SimpleNestedInteger(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    @Override
    public boolean isInteger() {
        return value != null;
    }

    @Override
    public Integer getInteger() {
        return value;
    }

    @Override
    public List<NestedInteger> getList() {
        return list;
    }
}

```

## Output:

<img width="773" height="216" alt="image" src="https://github.com/user-attachments/assets/4e9e4053-6036-40bc-bf9d-27fdcbecf6d6" />

## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
