# 0383. Ransom Note

## Approach 1: HashMap
Make a single pass over the letter of `ransomNote` and storing the frequency for each encountered character in HashMap. Next, we make a pass over the magazine string. When processing a character c, reduce its count by 1 if the character appear in HashMap. Remove it once the count goes to zero.

```Java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character, Integer> ransomNoteDict = new HashMap<>();
        
        for (char c : ransomNote.toCharArray()) {
            ransomNoteDict.put(c, ransomNoteDict.getOrDefault(c, 0) + 1);
        }
        
        for (char c : magazine.toCharArray()) {
            if (ransomNoteDict.containsKey(c)) {
                ransomNoteDict.put(c, ransomNoteDict.get(c) - 1);
                
                if (ransomNoteDict.get(c) == 0) {
                    ransomNoteDict.remove(c);
                }
            }
        }
        
        return ransomNoteDict.isEmpty();
    }
}
```

### Time and Space Complexity

N = length of magazine string
- Time: `O(N)`
- Space: `O(1)`
