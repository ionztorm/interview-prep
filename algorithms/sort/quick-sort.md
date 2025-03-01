- [Follow on Bluesky](https://bsky.app/profile/leonlonsdale.dev)
- [Join Discord](https://discord.gg/dhrdFh98UA)

# Quick Sort

## Quick Facts

- **Type:** Divide and Conquer, Recursive
- **In-Place:** ✅ Yes (with in-place partitioning)
- **Time Complexity:**
  - **Best & Average:** $O(n \log n)$
  - **Worst:** $O(n^2)$ (Unbalanced partitions)
- **Space Complexity:** $O(\log n)$ (due to recursion)

## How It Works

Quick Sort is an efficient **divide-and-conquer** sorting algorithm that organises elements by recursively partitioning the array.

1. A **pivot** element is chosen (commonly the last element).
2. The algorithm rearranges the array so that:
   - All elements **smaller** than the pivot are placed to its **left**.
   - All elements **larger** than the pivot are placed to its **right**.
3. This process is called **partitioning**, and once completed, the pivot is in its correct sorted position.
4. The algorithm then recursively applies the same process to the left and right partitions until the entire array is sorted.

## Pseudocode

### `partition()` Function Pseudocode

1. Choose a pivot element. Typically, the last element in the list is used as the pivot.
2. Initialise a variable `last_low_value_index` to track the position of the last smaller element (set it to `low - 1`).
3. Iterate through the list from `low` to `high - 1`:
   - If the current element is smaller than the pivot:
     - Increment `last_low_value_index` by 1.
     - Swap the current element with the element at `last_low_value_index`, ensuring smaller elements remain to the left.
4. After the loop, swap the pivot element with the element at `last_low_value_index + 1` to place it in its correct sorted position.
5. Return the index of the pivot.

---

### `quick_sort()` Function Pseudocode

1. If `low` is less than `high` (i.e., the list contains more than one element):
   - Call `partition()` to place one element in its correct sorted position.
   - Recursively apply `quick_sort()` to the left sub-list (elements before the pivot).
   - Recursively apply `quick_sort()` to the right sub-list (elements after the pivot).
2. The recursion continues until all sub-lists contain one or zero elements, at which point the list is fully sorted.

## Example Code

```python
def partition(arr, low, high):

	pivot = arr[high]
	last_low_value_index = low - 1

	for i in range(low, high):
		if arr[i] < pivot:
			last_low_value_index += 1
			if i != last_low_value_index:
				arr[i], arr[last_low_value_index] = arr[last_low_value_index], arr[i]

	arr[last_low_value_index + 1], arr[high] = arr[high], arr[last_low_value_index + 1]

	return last_low_value_index + 1

def quick_sort(arr, low, high):

	if low < high:
		pivot = partition(arr, low, high)
		quick_sort(arr, low, pivot - 1)
		quick_sort(arr, pivot + 1, high)
```

## ## Complexity

### Time Complexity

The time complexity of Quick Sort varies depending on how well the partitioning is balanced.

- **Best and Average Case: $O(n \log(n))$**

  - At each step, Quick Sort partitions the array around a pivot, dividing it into two smaller subarrays.
  - If the pivot is chosen well (e.g., near the median), the array is split roughly in half at each step, creating a balanced recursion tree with a depth of **$\log(n)$**.
  - Since each level of recursion processes all **$n$** elements (through partitioning), the total time complexity is **$O(n \log(n))$**.

- **Worst Case: $O(n^2)$**
  - If the pivot is always the smallest or largest element (as in an already sorted or reverse-sorted array when using the last element as the pivot), the partitions become highly unbalanced.
  - In this case, the recursion depth reaches **$O(n)$**, and each level processes all **$n$** elements, leading to a worst-case complexity of **$O(n^2)$**.
  - This issue can be mitigated by using **randomised pivot selection** or **median-of-three partitioning**.

---

### Space Complexity

Quick Sort has a **space complexity of $O(\log(n))$**, which is better than Merge Sort’s **$O(n)$**.

- **In-Place Sorting:**
  - Quick Sort does not require additional arrays for merging; instead, it swaps elements in place. This makes it much more memory-efficient than Merge Sort.
- **Recursive Call Stack:**
  - Quick Sort is a recursive algorithm, so it uses a call stack.
  - In the best and average cases, the recursion depth is **$O(\log(n))$** (since the array is split roughly in half each time).
  - In the worst case (highly unbalanced partitions), the recursion depth can reach **$O(n)$**, leading to **$O(n)$** space usage.
  - However, **tail recursion optimisation** and **hybrid approaches** (such as switching to insertion sort for small subarrays) can reduce stack space usage.

Thus, Quick Sort typically requires **only $O(\log(n))$ space**, making it more memory-efficient than Merge Sort.
