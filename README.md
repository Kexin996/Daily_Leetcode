# 75. Sort Colors

## PROBLEM

{% embed url="https://leetcode.com/problems/sort-colors/" %}

```java
class Solution {
    public void sortColors(int[] nums) 
    {
        // we define:
        // i: the elements before this index are red
        //    - we can also interpret it as the first white element index
        // j: the first index of unsorted element
        // k: the last index of unsorted element
        // (k,nums.length-1): elements that are blue
        int i = 0, j = 0, k = nums.length-1,temp = 0;
        while (j <= k)
        {
            temp = nums[j];
            if (temp == 0)
            {
                // swap nums[i],nums[j]
                nums[j] = nums[i];
                nums[i] = temp;
                
                // we swap the value but don't change the index
                // in order to fit our definition, we need to increase i
                // and j
                i++;
                j++;
            }
            else if (temp == 1)
            {
                j++;
            }
            else
            {
                // swap nums[j] and nums[k]
                nums[j] = nums[k];
                nums[k] = temp;
                
                // it still fulfills the condition
                // since as we swap, nums[k] is still an unsorted element
                // but now we enlarge [k+1,)
                // we decrease k.
                k--;

            }
        }
        return;
    }
}
```

## SHORT SUMMARY

* it is an updated version of the partition in quicksort
* **!!!!PAT ATTENTION TO THE DEFINITION OF EACH VARIABLE**
* TC: O(n)
* SC: O(1)
