# Selection Sort

## Quick Facts

- **Type:** Comparison-based, Iterative
- **In-Place:** ✅ Yes
- **Time Complexity:** $O(n^2)$ (Best, Average, Worst)
- **Space Complexity:** $O(1)$

## How It Works

- Selection Sort is an **in-place** sorting algorithm that repeatedly finds the smallest element in the unsorted part of the array and moves it to its correct position.
- The algorithm maintains a **variable to track the index of the smallest value** in the remaining unsorted portion of the list.
- An inner loop scans through the unsorted part, **comparing each element to the current lowest value**.
- When a new smallest value is found, the **index of the lowest element is updated**.
- After completing the scan, the smallest element is swapped with the element at the current position, **placing it in its correct sorted order**.
- This process repeats for every element in the array until the entire list is sorted.

## Pseudocode

1. Loop through the array from the first element to the last:
   1. Create a variable `index_of_lowest` and set it to the current index.
   2. Loop through the remaining unsorted part of the array:
      1. Compare each element with the current lowest value.
      2. If a smaller element is found, update `index_of_lowest` to its index.
   3. Swap the element at the current index with the element at `index_of_lowest`, placing the smallest value in its correct position.
2. Repeat this process until the entire array is sorted.

## Example Code

```python
def selection_sort(arr:list) -> list:
    for i in range(len(arr)):

        index_of_lowest = i

        for j in range(index_of_lowest, len(arr)):
            if arr[j] < arr[index_of_lowest]:
                index_of_lowest = j

        arr[i], arr[index_of_lowest] = arr[index_of_lowest], arr[i]

    return arr
```

## Time Complexity

Selection Sort always has a time complexity of **$O(n^2)$**, regardless of the initial order of the elements.

- **Worst Case: $O(n^2)$**

  - The worst-case scenario occurs when the array is sorted in **reverse order**, but the number of comparisons remains the same in all cases.
  - The algorithm must compare each element with every other element in the unsorted portion of the list.
  - Since there are **n** elements, and at each step, the algorithm scans the remaining **(n - 1), (n - 2), ... , 1** elements, the total number of comparisons is **$O(n^2)$**.

- **Best Case: $O(n^2)$**

  - Unlike some other sorting algorithms, Selection Sort does **not** take advantage of an already sorted list.
  - Even if the array is sorted, the algorithm still scans through all elements to find the minimum value at each step.
  - As a result, the best-case time complexity remains **$O(n^2)$**.

- **Average Case: $O(n^2)$**
  - Since Selection Sort performs the same number of comparisons regardless of the input order, its average-case complexity is also **$O(n^2)$**.
