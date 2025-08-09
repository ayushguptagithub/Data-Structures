
# 🟢 I. Linear Data Structures

Linear Data Structures store data sequentially so that each element is connected to its previous and next element.

**Examples:** Arrays, Linked Lists, Queues, Stacks.

---

## **1. Arrays**

An **Array** is a collection of elements stored in  **contiguous memory locations** .

Elements are accessed using index numbers (0-based in most programming languages).

---

### **1.1 Basics: Declaration, Input & Output**

**What is it?**

* **Declaration** means telling the compiler about the array’s **size** and  **data type** .
* **Input/Output** means storing and printing array elements.

**Where it’s used?**

* Storing **fixed-size lists** like marks, IDs, scores, etc.

**Why is it important?**

* **Fast access** : `O(1)` time for accessing an element by index.
* Foundation for advanced data structures.

**Example Problem:**

📌 Read an array of size `N` and print its elements in  **reverse order** .

```java
import java.util.*;

public class ArrayBasics {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];

        // Input
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        // Output in reverse
        for (int i = n - 1; i >= 0; i--) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

**Explanation:**

* **Input loop** → stores values in `arr`.
* **Reverse loop** → starts from `n-1` to `0`.

**Complexity:**

* Time: `O(N)` for input + `O(N)` for output
* Space: `O(N)` for storing the array

---

### **1.2 Insertion & Deletion**

**What is it?**

* **Insertion** : Adding an element at a given index.
* **Deletion** : Removing an element from a given index.

**Where it’s used?**

* Adding/removing items in an existing dataset.

**Why is it important?**

* Basic operation needed before implementing  **dynamic arrays** .

---

**Example Problem (Insertion at given position):**

```java
public class ArrayInsertion {
    public static void main(String[] args) {
        int[] arr = new int[6];
        int n = 5;
        int[] data = {1, 2, 3, 4, 5};
        for (int i = 0; i < n; i++) arr[i] = data[i];

        int pos = 2, value = 99;

        for (int i = n; i > pos; i--) {
            arr[i] = arr[i - 1];
        }
        arr[pos] = value;
        n++;

        for (int i = 0; i < n; i++) System.out.print(arr[i] + " ");
    }
}
```

**Explanation:**

* Shift all elements **right** from the insertion position.
* Place the new value.

**Complexity:**

* Time: `O(N)` (due to shifting)
* Space: `O(1)` (in-place)

---

**Example Problem (Deletion at given position):**

```java
public class ArrayDeletion {
    public static void main(String[] args) {
        int[] arr = {1, 99, 2, 3, 4, 5};
        int n = 6, pos = 1;

        for (int i = pos; i < n - 1; i++) {
            arr[i] = arr[i + 1];
        }
        n--;

        for (int i = 0; i < n; i++) System.out.print(arr[i] + " ");
    }
}
```

**Explanation:**

* Shift all elements **left** from the deletion position.

**Complexity:**

* Time: `O(N)`
* Space: `O(1)`

---

### **1.3 Traversals**

**What is it?**

Visiting each element in an array exactly once.

**Where it’s used?**

* Searching, printing, updating all elements.

**Why is it important?**

* Base for almost every array operation.

```java
for (int i = 0; i < arr.length; i++) 
    System.out.print(arr[i] + " "); // Forward

for (int i = arr.length - 1; i >= 0; i--) 
    System.out.print(arr[i] + " "); // Reverse
```

**Complexity:**

* Time: `O(N)`
* Space: `O(1)`

---

### **1.4 Prefix Sum**

**What is it?**

* An array that stores **cumulative sums** for  **fast range queries** .

**Where it’s used?**

* Finding sum of elements between indices quickly.
* Competitive programming, analytics, etc.

**Why is it important?**

* Reduces repeated summation from `O(N)` to `O(1)` for queries.

**Example Problem:**

📌 Given an array, find the sum of elements from index `l` to `r`.

```java
public class PrefixSum {
    public static void main(String[] args) {
        int[] arr = {2, 4, 6, 8, 10};
        int n = arr.length;
        int[] prefix = new int[n];

        prefix[0] = arr[0];
        for (int i = 1; i < n; i++) {
            prefix[i] = prefix[i - 1] + arr[i];
        }

        int l = 1, r = 3;
        int sum = prefix[r] - (l > 0 ? prefix[l - 1] : 0);
        System.out.println("Sum from " + l + " to " + r + " = " + sum);
    }
}
```

**Explanation:**

* `prefix[i]` stores sum from index `0` to `i`.
* Range sum = `prefix[r] - prefix[l-1]`.

**Complexity:**

* Preprocessing: `O(N)`
* Query: `O(1)`
* Space: `O(N)`

---

### **1.5 Suffix Sum**

**What is it?**

* Array where each index stores the sum from that index to the end.

**Where it’s used?**

* Problems involving sum from middle to end of array.

**Example Problem:**

📌 Find suffix sums of an array.

```java
public class SuffixSum {
    public static void main(String[] args) {
        int[] arr = {2, 4, 6, 8, 10};
        int n = arr.length;
        int[] suffix = new int[n];

        suffix[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffix[i] = suffix[i + 1] + arr[i];
        }

        for (int val : suffix) System.out.print(val + " ");
    }
}
```

**Complexity:**

* Time: `O(N)`
* Space: `O(N)`

---

### **1.6 Two Pointers Technique**

**What is it?**

* Use two indices to solve problems in a single pass.

**Where it’s used?**

* Pair sum, removing duplicates, merging arrays.

**Example Problem:**

📌 Find all pairs with sum = target.

```java
public class TwoPointers {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 6, 8, 9};
        int target = 10;
        int left = 0, right = arr.length - 1;

        while (left < right) {
            int sum = arr[left] + arr[right];
            if (sum == target) {
                System.out.println("Pair: " + arr[left] + ", " + arr[right]);
                left++;
                right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }
}
```

**Complexity:**

* Time: `O(N)`
* Space: `O(1)`

---

### **1.7 Sliding Window**

**What is it?**

* A window of `k` elements moves through the array to solve subarray problems efficiently.

**Where it’s used?**

* Maximum/Minimum sum subarray of size `k`.

**Example Problem:**

📌 Find sum of all subarrays of size `k`.

```java
public class SlidingWindow {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6};
        int k = 3, n = arr.length;

        int windowSum = 0;
        for (int i = 0; i < k; i++) windowSum += arr[i];
        System.out.println("Sum: " + windowSum);

        for (int i = k; i < n; i++) {
            windowSum += arr[i] - arr[i - k];
            System.out.println("Sum: " + windowSum);
        }
    }
}
```

**Complexity:**

* Time: `O(N)`
* Space: `O(1)`

---

### **1.8 Kadane’s Algorithm**

**What is it?**

* Finds maximum sum subarray in `O(N)` time.

**Where it’s used?**

* Stock price analysis, profit calculation, max segment sum.

**Example Problem:**

📌 Find maximum subarray sum.

```java
public class Kadane {
    public static void main(String[] args) {
        int[] arr = {-2, -3, 4, -1, -2, 1, 5, -3};
        int maxSum = arr[0], currSum = arr[0];

        for (int i = 1; i < arr.length; i++) {
            currSum = Math.max(arr[i], currSum + arr[i]);
            maxSum = Math.max(maxSum, currSum);
        }
        System.out.println("Maximum Subarray Sum: " + maxSum);
    }
}
```

**Complexity:**

* Time: `O(N)`
* Space: `O(1)`

---

### **1.9 Applications in Sorting & Searching**

Example: **Binary Search**

📌 Find if a number exists in a sorted array.

```java
public class BinarySearch {
    public static int search(int[] arr, int target) {
        int left = 0, right = arr.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) return mid;
            if (arr[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }
    public static void main(String[] args) {
        int[] arr = {1, 3, 5, 7, 9};
        int idx = search(arr, 7);
        System.out.println(idx != -1 ? "Found at " + idx : "Not found");
    }
}
```

**Complexity:**

* Time: `O(log N)`
* Space: `O(1)`

---

`<img src="![1754727908190](image/Arrays/1754727908190.png)">`
