# 0349. Intersection of Two Arrays

## Approach 1: Double-ended Queue
Sorted two input arrays. We can advancing throught the two sorted arrays in increasing order using two pointer. At each iteration, the duplicate value will be resolve by advance two pointer to the last duplicate value index and do comparison afterwards. If the array elements differ, the smaller one can be eliminated. If they are equal, we add that value to another list `ans` and advance both.

```Java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        List<Integer> ans = new ArrayList<>();
        int p1 = 0, p2 = 0;
        
        while (p1 < nums1.length && p2 < nums2.length) {
            while (p1 < nums1.length - 1 && nums1[p1] == nums1[p1 + 1]) p1++;
            while (p2 < nums2.length - 1 && nums2[p2] == nums2[p2 + 1]) p2++;
            
            if (nums1[p1] == nums2[p2]) {
                ans.add(nums1[p1]);
                p1++;
                p2++;
            } else if (nums1[p1] > nums2[p2]) {
                p2++;
            } else {
                p1++;
            }
        }
        
        return ans.stream().mapToInt(i -> i).toArray();
    }
}
```

### Time and Space Complexity

N = The longest length between two arrays, `nums1` and `nums2`
- Time: `O(N)`
- Space: `O(1)`
