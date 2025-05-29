##  Happy Number

- Write an algorithm to determine if a number n is happy.
- A happy number is a number defined by the following process:
- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
- Those numbers for which this process ends in 1 are happy.
- Return true if n is a happy number, and false if not.

```
Example 1:

Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

Example 2:

Input: n = 2
Output: false
```
 
**Constraints**:

- 1 <= n <= 231 - 1


## Brute Force :

- getDigitSquareSum calculates the sum of squares of digits of a number
- Uses a HashSet to track previously seen numbers to detect cycles
- Loop continues until current == 1 (happy number) or cycle is found
- If a cycle is detected (number repeats), returns false
- If number becomes 1, returns true (it's a happy number)
- Efficient for problem constraints, avoids infinite loops

```
class Solution {
    public int getDigitSquareSum(int number) {
        int sum = 0;
        while (number > 0) {
            int digit = number % 10;
            sum += digit * digit;
            number /= 10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        int current = n;
        HashSet<Integer> seenSums=new HashSet<>();
        while(current!=1){
            current=getDigitSquareSum(current);
            if (seenSums.contains(current)) {
                return false;
            }
            seenSums.add(current);
        }  
        return true;
        
    }
}
```

- **Time Complexity** - O(KlogK)
- **Space Complexity** - O(K)


## Fast and Slow Pointer

- getDigitSquareSum(int number) → Calculates sum of squares of digits of a number
- sum += digit * digit → Adds square of each digit to sum
- number /= 10 → Moves to the next digit (right to left)
- slow = n → Slow pointer starts at original number
- fast = getDigitSquareSum(n) → Fast pointer starts one step ahead
- while(fast != 1 && slow != fast) → Loop continues until happy (fast = 1) or cycle is found (slow == fast)
- slow = getDigitSquareSum(slow) → Slow moves one step
- fast = getDigitSquareSum(getDigitSquareSum(fast)) → Fast moves two steps
- return fast == 1 → Returns true if fast reaches 1, meaning number is happy


```
class Solution {
    public int getDigitSquareSum(int number) {
        int sum = 0;
        while (number > 0) {
            int digit = number % 10;
            sum += digit * digit;
            number /= 10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        int slow = n;
        int fast = getDigitSquareSum(n);
        while(fast!=1 && slow!=fast){
            slow=getDigitSquareSum(slow);
            fast=getDigitSquareSum(getDigitSquareSum(fast));
        }  
        return fast==1;
        
    }
}
```

- **Time Complexity** - O(KlogK)
- **Space Complexity** - O(1)
