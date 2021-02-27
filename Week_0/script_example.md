# Script example

the writing text of a algorithm problem
sequential set of steps that follow a relevant format.

## Example: remove Element from Array

Input: nums = [1,1,2]
Output: 2, nums = [1,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the returned length.

## FORMAT:

## _Hierarchy DS Big Oh:_

Brute force
(better for many invalid elements)

Two pointer
(rare invalid elements)

## _Edge Cases:_

What happens when the elements to remove are rare?

## _Brute Force APPROACH:_

nums = [3,2,2,3], val = 3,
Return length = 2 ([2,2,3,3])

nums = [1], val = 1
Return length = 0 ([1])

nums = [0], val = 1
Return length = 1 ([1])

## _Analysis:_
```
3  2  2  3  val = 3
3  2  2  3  i = 0
lo
2  2  2  3  i = 1
   lo
2  2  2  3  i = 2
      lo
2  2  2  3  i = 3
      lo (length)
```

It is better when elements to remove are so many. So the if would be skipped often.

## _Code:_

```
public int removeElement(int[] nums, int val) {
  int n = nums.length;
  int lo = 0;
  for (int i = 0; i < n; ++i) {
    if (nums[i] != val) {
      nums[lo] = nums[i];
      ++lo;
    }
  }
  return lo;
}
```

Time: O(N)
Space: O(1)


## _Two pointer APPROACH:_

This approach is better when elements to remove are rare. So the if would be skipped often.

We use two pointers lo and hi to solve this problem. lo points to the current element we are examining; hi is the current position we want to put invalid element at. See the example below for detail.

lo = points to the beginning 
hi = points to the end is the place where we want to put the element that don’t match with our val

```
val = 3
3  2  2  3
lo       hi
// Since the current element nums[lo] is invalid, we want to place it at where hi is currently pointing!
// After swapping, we decrease hi by 1, and it will point to a new position that we will put invalid element at.
```

## _Invariants_:

1 Invariant:

lo position = for all valid elements 
hi position = for all invalid elements

Someone may ask that by this swapping an invalid element nums[hi] = 3 would go to lo. It is okay, because if we do swapping we only update hi. However, lo stays where it used to be, so the invalid element will be considered in the next round.

Also, if lo does not point to an invalid element, we just increase lo by one to examine the next element.

2 Invariant:
base case examination

lo < hi or lo <= hi:

It is important to decide to use lo < hi or lo <= hi as our loop condition. Here is a trick to find out which one is correct.

Consider the following example:
```
// A
   0  1
  [1]     val = 1
  lo
hi
// B
  [0]     val = 1
     lo
  hi
```

If we use lo < hi, the loop will not be executed and always return lo (0) as the length, which is not correct in case B. By observation, if we use lo <= hi, the above cases are handled very well and we have an invariant that lo will always be the resulting length.

## _Code Two Points:_

```
public int removeElement(int[] nums, int val) {
  int n = nums.length;
  int lo = 0, hi = n - 1;
  while (lo <= hi) {
    if (nums[lo] == val) {
      swap(nums, lo, hi);  // swapping
      --hi;
    } else {
      ++lo;
    }
  }
  return lo;
}
private void swap(int[] nums, int i, int j) {
  int temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}
```

Time: O(N)
Space: O(1)


 



