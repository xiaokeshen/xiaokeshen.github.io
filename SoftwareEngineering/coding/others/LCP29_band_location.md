## LCP 31. LCP 29 Band location
### Problem  
[LCP 29 Band Location](https://leetcode-cn.com/problems/SNJvJP/)
### Discussion  
As the data size is 10^9. O(n) solution will get TLE. We need O(log n) or O(1) solution.
Basic steps:  
- Find the outlayers and get the total number of elements in the outlayer.
- For the current layer, discuss by cases: top, right, bottom and left
### Code
```cpp
class Solution {
public:
    int orchestraLayout(int num, int i, int j) {
        long long layer = min(min(i, num - i-1), min(j, num - j-1));
        /*
        outlayer 1: 4*(n - 1 - 2*0)
        outlayer 2: 4*(n - 1 - 2*1)
        outlayer 3: 4*(n - 1 - 2*2)
        */
        long long outside = layer == 0? 0 :4*((long long)num - 1)*layer - 2*(2+2*(layer-1))*(layer - 1);
        long long curr;
        long long width = num - 1 - 2*layer;
        // four cases
        /*
         A--------------------------B
         |                          |
         |                          |
         |                          |
         D--------------------------C
        A: (layer, layer)
        B: (layer, layer + width)
        C: (layer + width, layer + width)
        D: (layer + width, layer)
        */
        // special case, if width is 0, it means it is the last element.
        if (width == 0) return outside % 9 + 1;
        // top [A, B)
        if (i == layer && j < layer + width) {
            curr = outside + j - layer + 1;
        }
        // right [B, C)
        else if (i < layer + width && j == layer + width) {
            curr = outside + width +  i - layer + 1;
        }
        // bottom [C, D)
        else if (i == layer + width && j > layer ) {
            curr = outside + 2*width + layer + width - j + 1 ;
        }
        // left [D, A)
        else if (i > layer  && j == layer ) {
            curr = outside + 3*width +  layer + width - i + 1 ;
        }
        return (curr - 1) % 9 + 1;
    }
};
```
