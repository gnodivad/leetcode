# 0039. Combination Sum

## Approach 1: Backtracking
Define a recusive function with the base case of if `target == 0`, we can add the current combination `result` to the final list `results`. Other than the base case, we would then continue to explore the sublist of candidate as `[index ... n]`. For each candidate, we check it is fullfilled the requirement of `target >= candidate[i]` and add it to `result`. We can call the recursive function to find any combination is `target - candidate[i]`.

```Java
class Solution {
    List<List<Integer>> results;
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        results = new ArrayList<>();
        
        combinationSum(candidates, 0, target, new LinkedList<>());

        return results;
    }
    
    public void combinationSum(int[] candidates, int index, int target, LinkedList<Integer> result) {
        if (target == 0) results.add(new ArrayList<>(result));
        
        for (int i = index; i < candidates.length; i++) {
            if (target >= candidates[i]) {
                result.add(candidates[i]);
                
                combinationSum(candidates, i, target - candidates[i], result);
                
                result.removeLast();
            }
        }
    }
}
```

### Time and Space Complexity

N = Length of array `candidates`
- Time: `O(N)`
- Space: `O(N)`

## References
- EPI 17.1