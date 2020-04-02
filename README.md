# Largest rectangle in a histogram
## https://leetcode.com/problems/largest-rectangle-in-histogram

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![Largest Rectangle in a histogram](histogram_area.png?raw=true "Title")

# Implementation 1 : O(n^2)
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        int area = heights[0];
        for(int i = 0; i < heights.length; i++) {
            int minHeight = heights[i];
            area = Math.max(area, heights[i]);
            for(int j = i+1; j < heights.length; j++) {
                minHeight = Math.min(minHeight, heights[j]);
                if(minHeight == 0)
                    break;
                area = Math.max(area, minHeight * (j - i +1));
            }
        }
        return area;
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
1. https://leetcode.com/articles/largest-rectangle-in-histogram
2. https://tech.pic-collage.com/algorithm-largest-area-in-histogram-84cc70500f0c
