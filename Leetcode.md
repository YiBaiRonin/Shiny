**有序数组的 Two Sum** 


----------


[Leetcode ：167. Two Sum II - Input array is sorted (Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

```html
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

**题目描述：** 


----------


在有序数组中找出两个数，使它们的和为 target。

使用双指针，一个指针指向值较小的元素，一个指针指向值较大的元素。指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。

- 如果两个指针指向元素的和 sum == target，那么得到要求的结果；
- 如果 sum > target，移动较大的元素，使 sum 变小一些；
- 如果 sum < target，移动较小的元素，使 sum 变大一些。 

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        vector<int> res;
        while(left < right)
        {
            int sum = nums[left] + nums[right];
            if(sum == target)
            {
                res.push_back(left);
                res.push_back(right);
                break;
            }
            else if(sum < target)
                left++;
            else
                right--;
        }
        return res;
    }
};
```
**无序数组的 Two Sum** 


----------


https://leetcode-cn.com/problems/two-sum/

```html
Input: nums = {2, 7, 11, 15}, target = 9
Output: [0, 1]
```
**题目描述**

----------


给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int size = nums.size();
        vector<int> res;
        for(int i = 0; i < size; ++i)
        {
            for(int j = i + 1; j < size; ++j)
            {
                if(nums[i] + nums[j] == target)
                {
                    res.push_back(i);
                    res.push_back(j);
                    break;
                }
            }
        }
        return res;
    }
};
```