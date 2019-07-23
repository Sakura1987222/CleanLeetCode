    # CleanLeetCodeByJava
    
    001.Two Sum
    
```
    //本人解决方法
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
    //leetcode用时最短的解决方法
    class Solution {
        public int[] twoSum(int[] nums, int target) {
            int indexArrayMax = 2047;
            int[] indexArrays = new int[indexArrayMax + 1];
            int diff = 0;
            for (int i = 0; i < nums.length; i++) {
                diff = target - nums[i];
                if (indexArrays[diff & indexArrayMax] != 0) {
                    return new int[] { indexArrays[diff & indexArrayMax] - 1, i };
                }
                indexArrays[nums[i] & indexArrayMax] = i + 1;
            }
            throw new IllegalArgumentException("No two sum value");

        }
    }
    ```
    ```
    //leetcode耗费内存最少的解决方法
    class Solution {
        public int[] twoSum(int[] nums, int target) {
            List<Integer> lst=new LinkedList<>();
         for(int i=0;i<nums.length;i++)
         {
             for(int j=i+1;j<nums.length;j++)
             {
                 if(nums[i]+nums[j]==target)
                 {
                     lst.add(i);
                     lst.add(j);
                 return lst.stream().mapToInt(m->m).toArray();
                 }
             }
         }
            return new int[5];
        }
    }
    ```

