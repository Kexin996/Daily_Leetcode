# 1. Two Sum

## PROBLEM

{% embed url="https://leetcode.com/problems/two-sum/" %}

```java
class Solution {
    public int[] twoSum(int[] nums, int target) 
    {
        int[] ans = new int[2];
        Map<Integer,Integer> map = new HashMap<Integer,Integer>();
        for (int k = 0; k < nums.length;k++)
        {
            if (!map.containsKey(target-nums[k]))
            {
                map.put(nums[k],k);
            }
            else
            {
                ans[0] = map.get(target-nums[k]);
                ans[1] = k;
            }
        }
        return ans;  
    }
}
```

## SHORT SUMMARY

* map + index
* Note: **when we need to return the index and the size of the element in the array is huge, we cannot use constant space and cannot sort it ---> map**
* TC: O(n)
* SC: O(n)
