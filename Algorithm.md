## Given an integer x, return true if x is palindrome integer.
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

## Roman to Integer
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