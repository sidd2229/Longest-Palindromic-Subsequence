# Longest Palindromic Subsequence (LPS)

## 🧩 Problem Statement
Given a string `s`, the task is to find the length of the longest subsequence that forms a palindrome.  
A subsequence does not need to be contiguous, which makes this different from the Longest Palindromic Substring problem.

---

## 💡 Why This Problem Was Challenging
This problem was challenging because it required understanding how overlapping subproblems work in **interval-based Dynamic Programming**.  
My initial recursive approach resulted in exponential time complexity, so I needed a more optimized strategy.  
I referred to a few online resources and discussions to understand the correct recurrence relation and how to structure the DP table effectively.  
Identifying how the state transitions change based on character matches (`s[i] == s[j]`) versus mismatches was the biggest challenge.

---

## 🚀 Approach (Dynamic Programming – Interval DP)
- I used a **2D DP table** where `dp[i][j]` represents the length of the longest palindromic subsequence in the substring `s[i...j]`.
- **If characters match** (`s[i] == s[j]`):  
  `dp[i][j] = 2 + dp[i+1][j-1]`
- **If they do not match**:  
  `dp[i][j] = max(dp[i+1][j], dp[i][j-1])`
- I filled the DP table **bottom-up**, starting from smaller substrings and expanding outward.
- Visualizing the transitions helped ensure correctness and avoid common mistakes.

---

## 🧠 Recurrence Relation
```text
if s[i] == s[j]:
    dp[i][j] = 2 + dp[i+1][j-1]
else:
    dp[i][j] = max(dp[i+1][j], dp[i][j-1])
```



## 📘 Example
For the input:  
`s = "bbabcbcab"`

The Longest Palindromic Subsequence is `"babcbab"` with length **7**.

---

## 📂 Code

class Solution {
    public int longestPalindromeSubseq(String text1) {
        if (text1 == null || text1.length() == 0) return 0;

        String text2 = new StringBuilder(text1).reverse().toString();
        int n = text1.length();
        char[] a = text1.toCharArray();
        char[] b = text2.toCharArray();
        int[][] dp = new int[n+1][n+1];

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (a[i-1] == b[j-1]) dp[i][j] = 1 + dp[i-1][j-1];
                else dp[i][j] = Math.max(dp[i][j-1], dp[i-1][j]);
            }
        }
        return dp[n][n];
    }
}


## ⏱️ Time & Space Complexity
- **Time Complexity:** O(n²)  
- **Space Complexity:** O(n²)


## ✔ Summary
This problem helped me strengthen my understanding of **Dynamic Programming on strings**,  
especially how to design and interpret a 2D interval DP table.  
The final optimized solution is clean, efficient, and easy to extend to related problems.
