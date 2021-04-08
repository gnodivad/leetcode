# 0125. Valid Palindrome

## Approach 1: Two Pointers
Set two pointers and points them to each end of the string. This two pointers will traverse the whole string and cross path in the middle eventually. Besides that, the two pointers will ignore the non-alphanumeric characters and traverse further. Each time, we will check the character that points by two pointer is the same character.

```Java
class Solution {
    public boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;
        
        while (i < j) {
            while (i < j && !Character.isLetterOrDigit(s.charAt(i))) i++;
            while (i < j && !Character.isLetterOrDigit(s.charAt(j))) j--;
            
            if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) {
                return false;
            }
            
            i++;
            j--;
        }
        
        return true;
    }
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Palindrome%20Check)