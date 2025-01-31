# Quick Sort Algorithm (Java)

This repository contains an optimized implementation of the **Quick Sort algorithm** in Java, using **Hoare’s Partition Scheme** with **randomized pivot selection** for improved performance.

🚀 Features
- **Quick Sort with Hoare’s Partition** (More efficient than Lomuto’s)
- **Randomized Pivot Selection** (Prevents O(n²) worst-case complexity)
- **Swap Function for Cleaner Code**
- **Optimized Recursive Calls**
- **Time Complexity Analysis**

## 📌 How It Works
Quick Sort is a **divide-and-conquer** algorithm:
1. Select a **pivot** element (randomized for better efficiency).
2. **Partition the array** around the pivot:
   - Elements smaller than pivot go left.
   - Elements larger go right.
3. Recursively apply Quick Sort on both subarrays.

### **Hoare’s Partitioning vs. Lomuto’s**
| Partition Scheme | Swaps | Efficiency |
|------------------|--------|------------|
| **Lomuto** (Single Scan) | More Swaps | Slightly Slower |
| **Hoare** (Bidirectional Scan) | Fewer Swaps | Faster (Less Overhead) |

## 🛠️ Code Implementation
```java
import java.util.Random;

class Solution {
    static Random rand = new Random();

    // QuickSort Function
    static void quickSort(int arr[], int low, int high) {
        if (low >= high) return; // Base case
        
        int pi = hoarePartition(arr, low, high);
        
        quickSort(arr, low, pi);   // Sort left partition
        quickSort(arr, pi + 1, high); // Sort right partition
    }

    // Hoare’s Partition Scheme
    static int hoarePartition(int arr[], int low, int high) {
        int pivotIndex = low + rand.nextInt(high - low + 1);
        swap(arr, pivotIndex, low); // Random pivot selection

        int pivot = arr[low];
        int i = low - 1, j = high + 1;

        while (true) {
            do { i++; } while (arr[i] < pivot);
            do { j--; } while (arr[j] > pivot);

            if (i >= j) return j;
            swap(arr, i, j);
        }
    }

    // Swap function
    static void swap(int arr[], int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Main function to test the sorting
    public static void main(String[] args) {
        int arr[] = {10, 7, 8, 9, 1, 5};
        int n = arr.length;
        
        System.out.println("Original Array:");
        printArray(arr);
        
        quickSort(arr, 0, n - 1);
        
        System.out.println("\nSorted Array:");
        printArray(arr);
    }

    // Function to print an array
    static void printArray(int arr[]) {
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
    }
}
