## [Palindrome Number](https://leetcode.com/problems/palindrome-number/)
Given an integer x, return true if x is palindrome integer.

AlgorithmUtils.isPalindrome(14541);
%

```java
	public boolean isPalindrome(int x) {
		if (x<0 || (x!=0 && x%10==0)) return false;
		int rev = 0;
		while (x>rev){
			rev = rev*10 + x%10;
			x = x/10;
		}
		return (x==rev || x==rev/10);
	}
```
1. Output is [true]

## [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
- I can be placed before V (5) and X (10) to make 4 and 9. 
- X can be placed before L (50) and C (100) to make 40 and 90. 
- C can be placed before D (500) and M (1000) to make 400 and 900.

AlgorithmUtils.romanToInt("MCMXCIV");
%

```java
	public int romanToInt(String s) {
		int sum=0;
		if(s.indexOf("IV")!=-1){sum-=2;}
		if(s.indexOf("IX")!=-1){sum-=2;}
		if(s.indexOf("XL")!=-1){sum-=20;}
		if(s.indexOf("XC")!=-1){sum-=20;}
		if(s.indexOf("CD")!=-1){sum-=200;}
		if(s.indexOf("CM")!=-1){sum-=200;}
		
		char c[]=s.toCharArray();
		int count=0;
		
		for(;count<=s.length()-1;count++){
		   if(c[count]=='M') sum+=1000;
		   if(c[count]=='D') sum+=500;
		   if(c[count]=='C') sum+=100;
		   if(c[count]=='L') sum+=50;
		   if(c[count]=='X') sum+=10;
		   if(c[count]=='V') sum+=5;
		   if(c[count]=='I') sum+=1;
		   
	   }
	   return sum;   
	}
```
1. Output is [1994]

## [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".
AlgorithmUtils.longestCommonPrefix(["flower","flow","flight"]);
%

```java
public String longestCommonPrefix(String[] strs) {
    if(strs == null || strs.length == 0)    return "";
    String pre = strs[0];
    int i = 1;
    while(i < strs.length){
        while(strs[i].indexOf(pre) != 0)
            pre = pre.substring(0,pre.length()-1);
        i++;
    }
    return pre;
}
```
1. Output is [fl]

## [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
1) Open brackets must be closed by the same type of b
rackets.
2) Open brackets must be closed in the correct order.

AlgorithmUtils.isValid("{[]}");
%

```java
public boolean isValid(String s) {
	Stack<Character> stack = new Stack<Character>();
	for (char c : s.toCharArray()) {
		if (c == '(')
			stack.push(')');
		else if (c == '{')
			stack.push('}');
		else if (c == '[')
			stack.push(']');
		else if (stack.isEmpty() || stack.pop() != c)
			return false;
	}
	return stack.isEmpty();
}
```
1. Output is [true]


## [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

AlgorithmUtils.mergeTwoLists(list1 = [1,2,4], list2 = [1,3,4]);
%

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2){
		if(l1 == null) return l2;
		if(l2 == null) return l1;
		if(l1.val < l2.val){
			l1.next = mergeTwoLists(l1.next, l2);
			return l1;
		} else{
			l2.next = mergeTwoLists(l1, l2.next);
			return l2;
		}
}
```
1. Output is [1,1,2,3,4,4]

## [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.
 
AlgorithmUtils.removeDuplicates([0,0,1,1,1,2,2,3,3,4]);
%

```java
public int removeDuplicates(int[] nums) {
    int i = nums.length > 0 ? 1 : 0;
    for (int n : nums)
        if (n > nums[i-1])
            nums[i++] = n;
    return i;
}
```
1. Output is [5, nums = [0,1,2,3,4,_,_,_,_,_]]


## [Remove Element](https://leetcode.com/problems/remove-element/)
AlgorithmUtils.removeElement(nums = [0,1,2,2,3,0,4,2], val = 2);
%

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int idx =0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]!=val) {
				nums[idx++]=nums[i];
			}
        }
        return idx;
    }
}
```
1. Output is [5, nums = [0,1,4,0,3,_,_,_]]


##  [Length of Last Word](https://leetcode.com/problems/length-of-last-word/)
Given a string s consisting of some words separated by some number of spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

AlgorithmUtils.lengthOfLastWord("   fly me   to   the moon  ");
%

```java
    public int lengthOfLastWord(String s) {
        int length = 0;
		
		// We are looking for the last word so let's go backward
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) != ' ') { // a letter is found so count
                length++;
            } else {  // it's a white space instead
				//  Did we already started to count a word ? Yes so we found the last word
                if (length > 0) return length;
            }
        }
        return length;
    }
```
1. Output is [4]

## [Implement strStr() - indexOf method](https://leetcode.com/problems/implement-strstr/)
Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

AlgorithmUtils.strStr("hello","ll");
%

```java
	public int strStr(String haystack, String needle) {
	  for (int i = 0; ; i++) {
		for (int j = 0; ; j++) {
		  if (j == needle.length()) return i;
		  if (i + j == haystack.length()) return -1;
		  if (needle.charAt(j) != haystack.charAt(i + j)) break;
		}
	  }
	}
```
1. Output is [2]


## [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

AlgorithmUtils.searchInsert(nums = [1,3,5,6], target = 5);
%

```java
    public int searchInsert(int[] A, int target) {
        int low = 0, high = A.length-1;
        while(low<=high){
            int mid = (low+high)/2;
            if(A[mid] == target) return mid;
            else if(A[mid] > target) high = mid-1;
            else low = mid+1;
        }
        return low;
    }
```
1. Output is [2]

## [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

AlgorithmUtils.maxSubArray(nums = [-2,1,-3,4,-1,2,1,-5,4]);
%

```java
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int max = Integer.MIN_VALUE, sum = 0;
        
        for(int i=0;i<n;i++){
            sum += nums[i];
            max = Math.max(sum,max);
            
            if(sum<0) sum = 0;
        }
        
        return max;
    }
```
1. Output is [6]
