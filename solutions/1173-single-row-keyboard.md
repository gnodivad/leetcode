# 1173. Single-Row Keyboard

## Approach 1
Use HashMap to map the character to the index correctly. Iterate through `word` character by character and sum up the different of index between latest character with `initialKey`. The `initialKey` will set to the first character in `keyboard` at the begining and update it when we iterate through `word`.

```Java
class Solution {
    public int calculateTime(String keyboard, String word) {
        HashMap<Character, Integer> map = new HashMap<>();
        
        for (int i = 0; i < keyboard.length(); i++) {
            map.put(keyboard.charAt(i), i);
        }
        
        int time = 0;
        char initialKey = keyboard.charAt(0);
        for (char c : word.toCharArray()) {
            time += Math.abs(map.get(c) - map.get(initialKey));
            initialKey = c;
        }
        
        return time;
    }
}
```

### Time and Space Complexity

N = length of the string `keyboard`
- Time: `O(N)`
- Space: `O(1)`

## References
- None