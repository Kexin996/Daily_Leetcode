# Page 1

## PROBLEM

{% embed url="https://leetcode.com/problems/count-number-of-nice-subarrays/" %}

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) 
    {
        int start = 0, end = 0, count = 0,ans = 0; 
        // count is the subarrays containing exact k odd numbers in the window
        while (end < nums.length)
        {
            if (nums[end] % 2 == 1)
            {
                k--;
                // this will be useful when we enter the while loop
                // this condition is useful when it is 
                // triggered after we get the first
                // subarrays with k odd numbers
                // that means we need to shrink the window
                // so count = 0
                count = 0;
            }
            // at most ---> k will == 0
            // it will never be negative
            while ( k == 0)
            {
                if (nums[start] %2 == 1)
                {
                    k++;
                }
                start++;
                count++;
                // the count is used to record all the possible previous subarrays
            }
            // if count is not 0
            // it is like we just extend each available subarray by 1
            ans += count;  
            end++;
        }
        return ans;
    }
}
```

## SHORT SUMMARY

* dynamic window size + count + permutation
* TC: O(2n) ---> O(n)
* SC: O(1)
