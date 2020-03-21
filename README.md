# Largest rectangle in a histogram
## https://leetcode.com/problems/largest-rectangle-in-histogram

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

# Implementation 1 : O(n^2)
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int maxArea = 0;
        for (int i = 0; i < heights.length; i++) {
             int minHeight = heights[i];
            for (int j = i; j < heights.length; j++) {
                minHeight = Math.min(minHeight, heights[j]);
                maxArea = Math.max(maxArea, minHeight * (j - i + 1));
            }
            System.out.println("maxArea : " + maxArea);
        }
        return maxArea;
    }
}
```

# References :
https://leetcode.com/articles/largest-rectangle-in-histogram
