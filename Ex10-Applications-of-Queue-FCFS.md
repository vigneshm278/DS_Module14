# Flattening a Nested List Using an Iterator
## DATE: 04-09-2025
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1.Start the program.

2.Define an interface-like class NestedInteger that can represent either a single integer or a nested list.

3.Use a stack or recursion to flatten all integers from the nested list into a single list.

4.Store the flattened list and maintain an index to track the current element.

5.Implement next() to return the next integer and hasNext() to check if more integers exist.

6.Test the iterator with a sample nested list.

7.Stop the program.
## Program:
```
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: Vignesh M
RegisterNumber: 212223240176

import java.util.*;

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class NI implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    NI(Integer value) {
        this.value = value;
        this.list = null;
    }

    NI(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    public boolean isInteger() {
        return value != null;
    }

    public Integer getInteger() {
        return value;
    }

    public List<NestedInteger> getList() {
        return list;
    }
}

class NestedIterator implements Iterator<Integer> {
    private List<Integer> flattenedList = new ArrayList<>();
    private int index = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flatten(nestedList);
    }

    private void flatten(List<NestedInteger> nestedList) {
        for (NestedInteger ni : nestedList) {
            if (ni.isInteger()) {
                flattenedList.add(ni.getInteger());
            } else {
                flatten(ni.getList());
            }
        }
    }

    public Integer next() {
        return flattenedList.get(index++);
    }

    public boolean hasNext() {
        return index < flattenedList.size();
    }
}

public class FlattenNestedList {
    public static void main(String[] args) {
        List<NestedInteger> nestedList = new ArrayList<>();
        nestedList.add(new NI(1));
        List<NestedInteger> innerList = new ArrayList<>();
        innerList.add(new NI(2));
        innerList.add(new NI(3));
        nestedList.add(new NI(innerList));
        nestedList.add(new NI(4));

        NestedIterator i = new NestedIterator(nestedList);
        System.out.print("Flattened list: ");
        while (i.hasNext()) {
            System.out.print(i.next() + " ");
        }
    }
} 
*/
```

## Output:

<img width="594" height="90" alt="514429842-2ed02c84-5ea3-4a30-bd22-198ca361f5b2" src="https://github.com/user-attachments/assets/d1664638-b3c3-4f2a-99dd-eef7663175c4" />



## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
