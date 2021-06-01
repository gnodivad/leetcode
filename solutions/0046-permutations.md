# 0046. Permutations

## Approach 1: Backtracking
Iterate over the integers from index `i` to index `nums.length -1`. Place `i`-th integer into every different index in the array and generate all the permutation which start from `i+1`.

```Java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> permutations = new ArrayList<List<Integer>>();
        List<Integer> numList = Arrays.stream(nums).boxed().collect(Collectors.toList());
		getPermutations(0, numList, permutations);
		
        return permutations;
    }
    
    public void getPermutations(int i, List<Integer> array, List<List<Integer>> permutations) {
		if (i == array.size() - 1) {
			permutations.add(new ArrayList<>(array));
			return;
		}
		
		for (int j = i; j < array.size(); j++) {
			swap(array, i, j);
			getPermutations(i + 1, array, permutations);
			swap(array, i, j);
		}
	}
	
	public void swap(List<Integer> array, int i, int j) {
		Integer tmp = array.get(i);
		array.set(i, array.get(j));
		array.set(j, tmp);
	}
}
```

### Time and Space Complexity

N = length of array `nums`
- Time: `O(N!.N)`
- Space: `O(N!.N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Permutations)