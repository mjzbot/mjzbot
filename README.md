---
description: This is the section one of the course on SML
---

# SML: Standard ML

this is more of a test page:

```sml
auto a = 10

```

```cpp
codestruct ST_Tree {
  // range [lo, hi]
  int lo = 0;       // lower bound of the range
  int hi = 0;       // upper bound of the range
  int counter = 0;  // keep track if the range is available
  int length = 0;   // cache away the length of the range
  ST_Tree *left = nullptr;
  ST_Tree *right = nullptr;

  int getMidRange() const {
    return lo + (hi - lo) / 2;
  }

  bool hasLeftChild() const {
    return left != nullptr;
  }

  bool hasRightChild() const {
    return right != nullptr;
  }

  ST_Tree *leftChild() {
    if (!left)
      left = new ST_Tree({lo, getMidRange()});
    return left;
  }

  ST_Tree *rightChild() {
    if (!right)
      right = new ST_Tree({getMidRange(), hi});
    return right;
  }

  // x1 and x2 are the range to be queried
  // How the tree is structured:
  // the leaf nodes are the adjacent indices which form a range:
  // [lo, hi] = [1 2], [3 4], [10, 11] ...
  // Given a root of range [X, Y], it will be divided to two children:
  // left: [X, (Y-X)/2]  right: [(Y-X)/2, Y]
  // Example: Root: [0, 3]
  // *Root.left: [0, 1]  Root.right: [1, 3]
  //                 *right.left: [1,2] *right.right: [2,3]
  // * means leaf nodes
  // It's IMPORTANT to note that we are not keeping individual index as leaf nodes;
  // Each node, both leaf and parents, are RANGES! This is critical.
  int update(int x1, int x2, int val) {
    if (x1 >= x2)
      return 0;

    if (x1 == lo && x2 == hi)
      counter += val;
    else {
      // ask the left and right children to update accordingly
      leftChild()->update(x1, min(getMidRange(), x2), val);
      rightChild()->update(max(getMidRange(), x1), x2, val);
    }

    if (counter > 0)
      length = hi - lo;
    else {
      int leftLength = hasLeftChild() ? leftChild()->length : 0;
      int rightLength = hasRightChild() ? rightChild()->length : 0;
      length = leftLength + rightLength;
    }

    return length;
  }
};
```

## This is the first heading

{% hint style="info" %}
to give you a good hint on this
{% endhint %}

> <mark style="color:orange;">**I always likes quotes**</mark>

{% file src=".gitbook/assets/Chapter_1_Introducing_System_Design__News_Feed_System_v6.0.4 (1).pdf" %}
some PDF notes
{% endfile %}

![](<.gitbook/assets/super bowl 2022.jpeg>)

Pictures work nicely like above.
