# 0771. Jewels and Stones

## Approach 1: HashSet
Build a set by go through all the jewels. Go through all the stones by check with the set and increment the count if matches.

```Java
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        HashSet<Character> set = new HashSet<>();
        
        for (Character c : jewels.toCharArray()) {
            set.add(c);
        }
        
        int count = 0;
        
        for (Character c : stones.toCharArray()) {
            if (set.contains(c)) count++;
        }
        
        return count;
    }
}
```

### Time and Space Complexity

n = number of stones, k = number of jewels
- Time: `O(n)`
- Space: `O(k)`

## References
- None