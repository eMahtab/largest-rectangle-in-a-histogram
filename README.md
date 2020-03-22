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
                if(minHeight == 0)
                    break;
                maxArea = Math.max(maxArea, minHeight * (j - i + 1));
            }
            System.out.println("maxArea : " + maxArea);
        }
        return maxArea;
    }
}
```

# Implementation 2 : O(n)
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int index = 0;
        while (index < heights.length) {
            if (stack.empty() || heights[index] >= heights[stack.peek()]) {
                stack.push(index++);
            } else {
                int top = stack.pop();
                int width = stack.empty() ? index : index - stack.peek() - 1;
                maxArea = Math.max(maxArea, heights[top] * width);
            }
        }

        while (!stack.empty()) {
            int top = stack.pop();
            int width = stack.empty() ? index : index - stack.peek() - 1;
            maxArea = Math.max(maxArea, heights[top] * width);
        }

       return maxArea;
    }
}
```

# References :
https://leetcode.com/articles/largest-rectangle-in-histogram
