##  Longest Substring Without Repeating Characters

- Given a string s, find the length of the longest substring without duplicate characters.

```
Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
 
**Constraints**:

- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces.

## Brute Force

- Initialize res = 0 to keep track of the maximum length found.
- Loop through each character as the starting index i of the substring.
- For each i, start another loop from j = i to end of the string:
- Initialize length = 1 (length of current substring).
- Use a flag flag = true to check if characters are unique.
- Use a third loop from k = j - 1 to i:
- Check if s.charAt(j) is equal to any previous character s.charAt(k).
- If yes, set flag = false and break the loop (duplicate found).
- If not, increase length by 1.
- If flag is still true, update res = max(res, length).
- If a duplicate is found, break the inner loop early as longer substrings won't be valid.
- After all loops, return res as the length of the longest unique-character substring.

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int res=0;
        int n=s.length();
        for(int i=0;i<n;i++){
            for(int j=i;j<n;j++){
                int length=1;
                boolean flag=true;
                for(int k=j-1;k>=i;k--){
                    if(s.charAt(j)==s.charAt(k)){
                        flag=false;
                        break;
                    }
                    length++;
                }
                if(flag){
                    res=Math.max(res,length);
                }
                else{
                    break;
                }
            }
        }
        return res;
        
    }
}
```

- **Time Complexity** - O(N*N*N)
- **Space Complexity** - O(1)


## HashSet

- Initialize res = 0 to store the maximum length.
- Loop through each character i as the starting point of the substring.
- For each i, do the following:
- Create an empty HashSet<Character> to track seen characters.
- Initialize length = 0 for the current substring.
- Start an inner loop from j = i to end of string:
- If s.charAt(j) is not in the set:
- Add it to the set.
- Increment length by 1.
- Update res = max(res, length).
- If it is already in the set, break the inner loop (duplicate found).
- Return res after checking all starting positions.

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int res=0;
        int n=s.length();
        for(int i=0;i<n;i++){
            HashSet<Character> set=new HashSet<>();
            int length=0;
            for(int j=i;j<n;j++){
               if(!set.contains(s.charAt(j))){
                 length++;
                 res=Math.max(res,length);
                 set.add(s.charAt(j));
               }
               else{
                break;
               }
            }
        }
        return res;
        
    }
}

```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(N)

## HashSet and Sliding window Optimised

- Use two pointers left and right to maintain a sliding window.
- Use a HashSet to store characters in the current window to detect duplicates.
- Initialize res to store max length and length to track current window size.
- Loop while right < s.length(), if the character at right is already in the set, remove characters from the left until it's gone.
- If no duplicate, add the character at right to the set, increase length, update res, and move right forward.
- Continue this until all characters are processed.
- Return res as the final answer.

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int left=0,right=0,res=0,length=0;
        HashSet<Character> set=new HashSet<>();
        while(right<s.length()){
            while(set.contains(s.charAt(right))){
                set.remove(s.charAt(left));
                left++;
                length--;
            }
            set.add(s.charAt(right));
            length++;
            res=Math.max(res,length);
            right++;
        }
        return res;       
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)

## HashMap and sliding Window optimised

- Initialize left, right, and res as 0 to control window and store result.
- Use a HashMap<Character, Integer> to store the last seen index of each character.
- Loop while right is less than string length.
- If current character is already in map, update left to max(left, map.get(char) + 1) to skip over the previous duplicate.
- Update or insert the character and its index into the map.
- Calculate current window length as right - left + 1 and update res with the max length.
- Increment right to expand the window.
- After loop, return res.

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int left=0,right=0,res=0;
        HashMap<Character,Integer> map=new HashMap<>();
        while(right<s.length()){
            if(map.containsKey(s.charAt(right))){
                left=Math.max(left,map.get(s.charAt(right))+1);
            }
            map.put(s.charAt(right),right);
            res=Math.max(res,right-left+1);
            right++;
        }
        return res;       
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)
