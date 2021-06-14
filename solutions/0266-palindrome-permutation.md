# 0266. Palindrome Permutation

## Approach 1
Traverse over the given string `s`, calculate the occurences of each of the character and stored them in HashMap. At the end, we traverse over the HashMap and find the number of characters with odd number of occurences. If the count happens to less than 2, we can conclude that a palindromic permutation is possible for s.

```Java
class Solution {
    public boolean canPermutePalindrome(String s) {
        HashMap<Character, Integer> counts = new HashMap<>();
        
        for (Character c : s.toCharArray()) {
            counts.put(c, counts.getOrDefault(c, 0) + 1);
        }
        
        int oddPair = 0;
        for (Map.Entry<Character, Integer> entry : counts.entrySet()) {
            int frequency = entry.getValue();
            oddPair += frequency % 2;
        }
        
        return oddPair <= 1;
    }
}
```

### Time and Space Complexity

N = length of the string `s`
- Time: `O(N)`
- Space: `O(1)`

## References
- EPI 7.5