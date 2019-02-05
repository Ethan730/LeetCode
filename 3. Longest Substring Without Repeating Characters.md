地址：https://leetcode.com/problems/longest-substring-without-repeating-characters/

# 题目：

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

# 理解：

求一个字符串的最长子串，该子串中不包含重复的元素。

# 思路：

注意一个性质，若s[i:j]有重复字母，则所有包含其的子串一定有重复。因此考虑所有两头相同的子串就可以了。map中记录上一次出现的位置，i表示非重复子串的起始位置。

# 实现：

1. C++

```cpp
class Solution {
public:
	int lengthOfLongestSubstring(string s) {
		unordered_map<char, int> m;
		int ans = 0;
		for (int i = 0, j = 0; j < s.length(); ++j) {
			if (m.count(s[j])) {
				i = max(i, m[s[j]]);
			}
			ans = max(ans, j - i + 1);
			m[s[j]] = j + 1;
		}
		return ans;
	}
};
```

2. Go

```go
func lengthOfLongestSubstring(s string) int {
	m := make(map[byte]int)
	ans := 0
	for i, j := 0, 0; j < len(s); j++ {
		tmp, ok := m[s[j]]
		if ok {
			if tmp > i {
				i = tmp
			}
		}
		if j-i+1 > ans {
			ans = j - i + 1
		}
		m[s[j]] = j + 1
	}
	return ans
}
```

用map还是会慢一些，当字符有限的时候，换成内置数组

```go
func lengthOfLongestSubstring(s string) int {
    m := make([]int, 128)
	ans := 0
	for i, j := 0, 0; j < len(s); j++ {
        if m[s[j]]!=0 {
			if m[s[j]] > i {
				i = m[s[j]]
			}
		}
		if j-i+1 > ans {
			ans = j - i + 1
		}
		m[s[j]] = j + 1
	}
	return ans
}

```