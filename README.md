# Quiz 3 Practice Answers
1)

DFS Pre-order: 10, 3, 1, 7, 12, 13, 15
DFS In-order: 1, 3, 7, 10, 12, 13, 15
DFS Post-order: 1, 7, 3, 15, 13, 12, 10
BFS: 10, 3, 12, 1, 7, 13, 15

2)
```java
public void mirror() 
{
        mirror(root);
}

private void mirror(BTNode<E> localRoot) 
{
        if (localRoot == null) return;
        mirror(myRoot.left);
        mirror(myRoot.right);
        BTNode<E> temp = localRoot.right;
        localRoot.right = localRoot.left;
        localRoot.left = temp;
}
```

3) For a Tree t, the lowest common connection for node 7 and node 13 will be
node 10. Find the common connection of any 2 nodes or return -1 if there isn't one.
```text
    10
   / \
  3  12
 / \   \
1   7   13
         \
          15

```
```java
public static int sameAncestor(Tree t, int x, int y) 
{
    if (t == null) 
    {
        return 0;
    }
    boolean here = (t.value() == x) || (t.value() == y);
    int a = commonAncestor(t.leftChild(), x, y);
    int b = commonAncestor(t.rightChild(), x, y);
    if ((a == -1 && b == -1) || ((a == -1 || b == -1) && here)) 
    {
    //The current node is the common ancestor if
    // 1. x and y are located on different branches
    // 2. one of x or y is the current label and the other is farther
    // down the tree
        return t.value();
    } 
    else if (here) 
    {

        // We "flag" this node by sending -1 up the recursive calls
        return -1;
    } else 
    {
        // If the node is not the common ancestor nor contains x/y as a label,
        // we can just pass up values from recursive calls as are
        return a + b;
    }
}
```


4) Given both implementations of a min and max heap, convert a max heap into a min heap without recursion.

```java
public static ArrayList<Integer> convertMaxHeapToMinHeap(ArrayList<Integer> maxHeap) {
    // Traverse the max heap from the last parent to the root
    for (int i = (maxHeap.size() / 2) - 1; i >= 0; i--) {
        // Perform a top-down heapify starting from each parent
        int j = i;
        while (true) {
            // Find the index of the minimum child
            int leftChild = 2 * j + 1;
            int rightChild = 2 * j + 2;
            int minChild = leftChild;

            if (rightChild < maxHeap.size() && maxHeap.get(rightChild) < maxHeap.get(leftChild)) {
                minChild = rightChild;
            }

            // Swap the current node with the minimum child if it is larger
            if (minChild < maxHeap.size() && maxHeap.get(minChild) < maxHeap.get(j)) {
                int temp = maxHeap.get(j);
                maxHeap.set(j, maxHeap.get(minChild));
                maxHeap.set(minChild, temp);
            } else {
                break;
            }

            // Update the index to continue the top-down heapify
            j = minChild;
        }
    }
    return maxHeap;
}
```


