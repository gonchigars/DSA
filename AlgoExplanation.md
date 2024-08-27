1. Prefix Sum

Imagine you have a line of piggy banks, each containing some coins. You want to know how many coins are in any range of piggy banks quickly.

Piggy banks:   [3]  [1]  [4]  [1]  [5]  [9]
Positions:      1    2    3    4    5    6

Instead of counting every time, you can create a new line where each piggy bank contains all the coins from itself and the previous ones.

Original:      [3]  [1]  [4]  [1]  [5]  [9]
Prefix Sum:    [3]  [4]  [8]  [9] [14] [23]

Now, if you want to know the sum of coins from position 2 to 4, you can simply subtract:
Sum(2 to 4) = Prefix[4] - Prefix[1] = 9 - 3 = 6

This way, you can answer any range sum query in constant time!

2. Two Pointer

Think of two pointer technique as having two fingers on a book page, moving independently to find something.

Let's say you have a sorted list of numbers, and you want to find two numbers that add up to a target sum.

Numbers:  1   3   4   6   8   9   11
Pointers: ^                       ^
          L                       R

Start with one finger (L) at the beginning and one (R) at the end. If the sum is too small, move L right. If it's too big, move R left. Keep doing this until you find the answer or the fingers meet.

3. Sliding Window

Imagine you're looking at a long strip of paper through a small window frame. You slide this frame along the strip to examine different parts.

Paper strip: [2] [1] [5] [1] [3] [2]
Window:      [   ]
              Slide ->

You might use this to find the subarray with the largest sum of a specific size, or the longest subarray with a certain property.

4. Modified Binary Search

Regular binary search is like finding a page in a book: you open it in the middle, decide if you need to go left or right, and repeat.

Modified binary search is for trickier books. Imagine a book where some pages are upside down:

Normal:     1  2  3  4  5  6  7  8  9
Rotated:    6  7  8  9  1  2  3  4  5
            ^        ^           ^
            L        M           R

You still divide and conquer, but you need extra checks. Is the middle (M) in the normal or rotated part? Which part contains your target?

For example, if you're looking for 3:
1. Check if M (9) is your target. It's not.
2. Is the left side (L to M) sorted? Yes.
3. Is your target in this sorted range? No.
4. So, it must be in the right side. Move L to M+1 and repeat.

These techniques are powerful tools in a programmer's toolkit. They help solve complex problems by breaking them down into manageable steps, often improving the efficiency of algorithms significantly.
