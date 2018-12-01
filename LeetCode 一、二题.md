# LeetCode 一、二题  
## 第一题    
思路：在第一次遍历的时候用Map来记录遍历过的节点的信息，其次再遍历一次来看看之前是否有满足条件的数据  

难点：很难想到用Map中的key来保存第一次遍历的每一个数据和target的差  

优化：可以边遍历边查看之前是否有匹配的  

	class Solution {
	    public int[] twoSum(int[] nums, int target) {
	        Map<Integer, Integer> map = new HashMap<Integer, Integer>();  //key代表该数据和target的差值，或者说是希望的目标值；value则是该数据在nums中的位置
	        
	        if (nums == null) {
	            return new int[2];
	        }
	        
	        for (int i = 0; i < nums.length; i++) {
	            Integer key = target - nums[i];
	            map.put(key, new Integer(i));
	        }
	        
	        for (int i = 0; i < nums.length; i++){
	            Integer node = nums[i];
	            if (map.get(node) != null) {
	                int d = map.get(node);
	                if(d != i) {
	                     return new int[]{d,i};
	                }
	            }
	        }
	        
	        return new int[2];
	        
	    }
	}  

优化：  

	class Solution {
	    public int[] twoSum(int[] nums, int target) {
	        Map<Integer, Integer> map = new HashMap<Integer, Integer>();    //key代表该数据和target的差值，或者说是希望的目标值；value则是该数据在nums中的位置
		        
		        if (nums == null) {
		            return new int[2];
		        }
		        
		        for (int i = 0; i < nums.length; i++) {
					if (map.get(new Integer(nums[i])) != null) {
						int[] result = new int[2];
						result[0] = map.get(new Integer(nums[i]).intValue());
						result[1] = i;
						return result;
					}
					Integer key = target - nums[i];
					if (map.get(key) == null) {
						map.put(key,i);
					}
				}	        
		        return new int[2];
        
    	}
	}

## 第二题  
思路：直接逐位相加，只是需要记录一下是否有进位的问题  

难点：各种情况需要考虑  

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
	        
	        int up = 0;
	        ListNode result = new ListNode((l1.val + l2.val) % 10);
	        up = (l1.val + l2.val) / 10;
	        ListNode current = result;
	        l1 = l1.next;
	        l2 = l2.next;
	        while (l1 != null && l2 != null) {
	            ListNode node = new ListNode((l1.val + l2.val + up) % 10);
	            up = (l1.val + l2.val + up) / 10;
	            current.next = node;
	            current = current.next;
	            l1 = l1.next;
	            l2 = l2.next;
	        
	        }
	    
	        
	        if (l1 == null && l2 != null) {
	            while (l2 != null){
	                ListNode node = new ListNode((l2.val + up) % 10);
	                up = (l2.val + up) / 10;
	                current.next = node;
	                current = current.next;
	                l2 = l2.next;
	            }
	        }
	        
	        if (l1 != null && l2 == null) {
	            while (l1 != null){
	                ListNode node = new ListNode((l1.val + up) % 10);
	                up = (l1.val + up) / 10;
	                current.next = node;
	                current = current.next;
	                l1 = l1.next;
	            }
	        }
	        
	        if(up > 0) {
	            ListNode node = new ListNode((up) % 10);
	            current.next = node;
	        }
	        return result;
	        
	    }
	}  
