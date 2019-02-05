地址：https://leetcode.com/problems/two-sum/
# 题目：

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

> Given nums = [2, 7, 11, 15], target = 9,
>
> Because nums[0] + nums[1] = 2 + 7 = 9,
> return [0, 1].

#  理解：
寻找两个数的和等于个特定target的对应下标。

# 思路：

从左到右，用一个哈希表记录元素和出现位置。判断哈希表中有没有值为`target-nums[i]`的元素，如果有，就返回结果。如果没有，把当前的`nums[i]`加入哈希表。

# 实现：

1. C++

```cpp
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> m;
		for (int i = 0; i<nums.size(); ++i) {
			if (m.count(target - nums[i]))
				return{ m[target - nums[i]],i };
			m[nums[i]] = i;
		}
	}
};
```

2. Go

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)
    res := []int{}
    for i, num := range nums {
        if left, ok := m[target-num]; ok {
            res = []int{left, i}
            return res
        }
        m[num] = i
    }
    return res   
}
```

