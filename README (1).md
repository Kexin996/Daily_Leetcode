# 151. Reverse Words in a String

{% embed url="https://leetcode.com/problems/reverse-words-in-a-string" %}

```java
// two solutions
// Stack version:
class Solution {
    public String reverseWords(String s) 
    {
        s = s.trim();
        Stack<String> stack = new Stack<String>();
        int i = 0, j = 0;
        while (i < s.length())
        {
            while (s.charAt(i) == ' ')
            {
                i++;
                j++;
            }
            while (j < s.length() && s.charAt(j) != ' ')
            {
                j++;
            }
            stack.push(s.substring(i,j));
            i = j;
            j = i;
        }
        StringBuilder ans = new StringBuilder();
        while (!stack.isEmpty())
        {
            ans.append(" ");
            ans.append(stack.pop());         
        }
        return ans.toString().substring(1);
    } 
}
```

* TC: O(n) ---> we only loop the string once and throw off the elements in the stack once, and the substring() method, and trim() method, is also O(n)
* SC: O(n) ---> we have an auxiliary stack

```java
// In-place reversal
class Solution {
    public String reverseWords(String s) 
    {
        char[] arr = s.toCharArray();
        // we first reverse the whole char array
        reverse(arr,0,arr.length-1);
        // then we try to clean the whole array
        // and reverse the words
        return cleaning(arr);
       
    } 
    public void reverse(char[] arr, int s, int e)
    {
        if (e < s)
        {
            return;
        }
        int i = s, j = e;
        while (j-i >= 1)
        {
            char temp = arr[j];
            arr[j] = arr[i];
            arr[i] = temp;
            i++;
            j--;
        }
        
    }
    public String cleaning(char[] arr)
    {
        // use c to check for the spaces that we should 
        // jump over
        int i = 0, c = 0;
        while (c < arr.length)
        {
            int j = i;
            while (c < arr.length && arr[c] == ' ')
            {
                c++;
            }
            while (c < arr.length && arr[c] != ' ')
            {
                arr[i++] = arr[c++];
            }
            reverse(arr,j,i-1);
            // why do we need this step:
            // e.g. [d,o,g,' ',' ',' ']
            // we can effectiely take off the blank space  
            // in the beginning of the array
            // but we need to deal with the situation
            // like how to add blank space 
            // when there is one / a group of trailing space 
            
            // when there is a trailing space, this while statement
            // will make c = arr.length
            while (c < arr.length && arr[c] == ' ')
            {
                c++;
            }
            
            // this if-statement can eliminiate 
            // the trailing space
            if (c < arr.length)
            {
                // this step is only for adding space interval
                arr[i++] = ' ';
            }
        }
        // we only need the elements from 0 to i-1
        // regardless of what value arr[i] takes
        // we don't need it
        
        return new String(arr, 0, i);
    }
}
```

* TC = O(n) ---> the whole reversion takes O(n), and the cleaning() takes O(n) \[we just reverse each word itself and add spaces]
* SC: O(1) ---> only use the auxiliary char\[] array

