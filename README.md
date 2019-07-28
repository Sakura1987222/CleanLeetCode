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

	2. Add Two Numbers
```
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    	//指向头(废结点)
        ListNode resultListNode = new ListNode(0);
        //移动指针
        ListNode curr = resultListNode;
        //存放进位(十位）
        int ten = 0;
        //ten != 0 :进位也要生成一个结点
        while(l1 != null || l2 != null || ten != 0) {
            ten += (l1 == null ? 0 : l1.val) + (l2 == null ? 0 : l2.val);
            //存个位
            curr.next = new ListNode(ten % 10);
            curr = curr.next;
            //存十位
            ten /= 10;
            l2 = l2 == null ? l2 : l2.next;
            l1 = l1 == null ? l1 : l1.next;;
        }
        //去掉废结点
        return resultListNode.next;
    }
}
```
        3. Longest Substring Without Repeating Characters
```
//本人解决方法
class Solution {
    public int lengthOfLongestSubstring(String s) {
        char[] chars = s.toCharArray();
        Map<Character, Integer> map = new HashMap<>(256);
        int max = 0, index = 0, lastIndex = 0, size;
        for (int i =0; i < chars.length; i++) {
            size =map.size();
            lastIndex = map.get(chars[i]) == null ? 0 : map.get(chars[i]);
            map.put(chars[i], i);
            if (size == map.size() && lastIndex != i && index <= lastIndex) {
                max = i - index > max ? i - index : max;
                if (chars.length - 1 - (i = index = lastIndex) <= max) return max;
                index++;
            }
            if (i == chars.length -1) return chars.length -index;
        }
        return max;
    }
}

#leetcode（改进版）
#主要思路：将不重复的元素放入到数组里，遇到重复的删除到上一次重复的元素
class Solution {
        public int lengthOfLongestSubstring(String s) {
            int Max = 0,count=0;
            ArrayList<Character> ar = new ArrayList<>();
            for(int i=0;i<s.length();i++){
                if(ar.contains(s.charAt(i))){
                    char ch = s.charAt(i);
                    while(ar.get(0) != ch){
                        ar.remove(ar.get(0));
                    }
                    ar.remove(0);
                    ar.add(s.charAt(i));
                    count = ar.size();
                    if(Max >= s.length() + count - i -1)
                        return Max;
                }else{
                    ar.add(s.charAt(i));
                    count = ar.size();
                    if(Max<count)
                        Max = count;
                }
            }
            return Max;
        }
    }

#leetcode用时最短的解决方法(改进版)
#主要思路：set里存放的是元素对应的下标，start存放的是不重复子列的开始下标。
#第一次存放元素其下标必定不可能大于start，存放重复且大于start的元素才会重设start
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] set = new int[128];
        char[] cs = s.toCharArray();
        int start = 0, max = 0;
        for (int i = 0; i < cs.length; i++){
            if (set[cs[i]] > start)
                start = set[cs[i]];
            //max = Math.max(max, i-start+1);
            if((i-start+1)>max)
                max=i-start+1;
            set[cs[i]] = i + 1;
        }
        return max;
    }
}

```

