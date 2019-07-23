    # CleanLeetCodeByJava
    
    001.Two Sum
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0;i < nums.length;i++) {
            Integer otherIndex = map.get(target - nums[i]);
            if (otherIndex != null) {
                return new int[] {i, otherIndex};
            }
            //防止元素重复
            map.put(nums[i], i);
        }
        return null;
    }
}
```
