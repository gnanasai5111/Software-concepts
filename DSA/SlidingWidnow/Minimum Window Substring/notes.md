##  Minimum Window Substring

- Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window.
- If there is no such substring, return the empty string "".
- The testcases will be generated such that the answer is unique.

```
Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.

Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```
 
**Constraints**:

- m == s.length
- n == t.length
- 1 <= m, n <= 105
- s and t consist of uppercase and lowercase English letters.

## Brute Force

- Builds a frequency map targetMap for characters in string t.
- Uses two nested loops to check every substring of s starting from index i.
- For each substring starting at i, builds a sourceMap frequency map.
- Checks if sourceMap contains all characters from targetMap with required frequencies.
- If condition satisfied, updates minimum length window and stores start and end indices.
- Returns the minimum window substring if found, else returns empty string.

```
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> targetMap = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            targetMap.put(t.charAt(i), targetMap.getOrDefault(t.charAt(i), 0) + 1);
        }
        int min = Integer.MAX_VALUE;
        int start = -1;
        int end = -1;
        for (int i = 0; i < s.length(); i++) {
            HashMap<Character, Integer> sourceMap = new HashMap<>();
            for (int j = i; j < s.length(); j++) {
                sourceMap.put(s.charAt(j), sourceMap.getOrDefault(s.charAt(j), 0) + 1);
                boolean flag = true;
                for (Character k : targetMap.keySet()) {
                    if (sourceMap.getOrDefault(k, 0) < targetMap.get(k)) {
                        flag = false;
                        break;
                    }
                }
                if (flag) {
                    if (j - i + 1 < min) {
                        min = Math.min(min, j - i + 1);
                        start = i;
                        end = j+1;
                    }
                    break;
                }
            }
        }
        return start == -1 ? "" : s.substring(start, end);

    }
}
```

- **Time Complexity** - O(N*N*M)
- **Space Complexity** - O(N+M)


## HashMap and sliding Window optimised

- Builds targetMap to store frequency of each character in string t.
- Uses a sliding window with two pointers: left and right.
- Maintains sourceMap to track character frequencies in the current window.
- required keeps count of unique characters needed to match.
- formed tracks how many characters currently meet the required frequency.
- Expands window by moving right and updates counts.
- When all required characters are matched (formed == required), attempts to shrink the window by moving left.
- Updates the minimum window if a smaller valid window is found.
- Returns the smallest valid window substring or empty string if not found.

```
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> targetMap = new HashMap<>();
        HashMap<Character, Integer> sourceMap = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            targetMap.put(t.charAt(i), targetMap.getOrDefault(t.charAt(i), 0) + 1);
        }
        int required=targetMap.size();
        int formed=0;
        int min = Integer.MAX_VALUE;
        int start = -1;
        int end = -1;
        int left=0,right=0;
        while(right<s.length()){
            char r=s.charAt(right);
            if(targetMap.containsKey(r)){
                sourceMap.put(r, sourceMap.getOrDefault(r, 0) + 1);
                if(targetMap.get(r).intValue()==sourceMap.get(r).intValue()){
                    formed++;
                }
            }
            while(left<=right && formed==required){
                char l=s.charAt(left);
                int length=right-left+1;
                if(length<min){
                    min=length;
                    start=left;
                    end=right+1;
                }

                if(sourceMap.containsKey(l)){
                    sourceMap.put(l, sourceMap.getOrDefault(l, 0) - 1);
                    if(targetMap.get(l).intValue() > sourceMap.get(l).intValue()){
                        formed--;
                    }
                }
                left++;
            }
            right++;
        }
        return start==-1?"":s.substring(start,end);

    }
}
```

- **Time Complexity** - O(N+M)
- **Space Complexity** - O(N+M)
