## **有序数组的 Two Sum** 


----------


[Leetcode ：167. Two Sum II - Input array is sorted (Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

```html
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

**题目描述：** 

在有序数组中找出两个数，使它们的和为 target。

使用双指针，一个指针指向值较小的元素，一个指针指向值较大的元素。指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。

- 如果两个指针指向元素的和 sum == target，那么得到要求的结果；
- 如果 sum > target，移动较大的元素，使 sum 变小一些；
- 如果 sum < target，移动较小的元素，使 sum 变大一些。 

```c++
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
## **无序数组的 Two Sum** 


----------


[Leetcode：1 无序数组的 Two Sum](https://leetcode-cn.com/problems/two-sum/)

```html
Input: nums = {2, 7, 11, 15}, target = 9
Output: [0, 1]
```
**题目描述**

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

```c++
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

## **两个数的平方之和**
[Leetcode：633 两个数的平方和](https://leetcode-cn.com/problems/sum-of-square-numbers/)

----------
**题目描述**
给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c。

```html
Input: 5
Output: 1 * 1 + 2 * 2 = 5
```
```c++
class Solution {
public:
    bool judgeSquareSum(int c) {
        long long left = 0;
        long long right = sqrt(c);
        while(left <= right)
        {
            long long sum = left * left + right * right;
            if(sum == c)
                return true;
            else if(sum > c)
                right--;
            else
                left++;
        }
        return false;
    }
};
```
## **反转字符串中的元音字符**
[Leetcode：345 反转字符串中的原因字符](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

----------
**题目描述**

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

```html
Input: "hello"
Output: holle
```
```c++
class Solution {
public:
    bool isAeiou(char c)
    {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' || \
            c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U';
    }
    string reverseVowels(string s) {
        int left = 0, right = s.size() - 1;
        while(left < right)
        {
            if(!isAeiou(s[left]))
                left++;
            else if(!isAeiou(s[right]))
                right--;
            else if(isAeiou(s[left]) && isAeiou(s[right]))
            {
                swap(s[left], s[right]);
                left++;
                right--;
            }
        }
        return s;
    }
};
```

## **验证回文子串**

[Leetcode ：680 验证回文子串](https://leetcode-cn.com/problems/valid-palindrome-ii/submissions/)


**题目描述**

给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。


```html
Input: aba
Output: true
Input: abca
Output: true
```
```c++
class Solution {
public:
    bool isPalindrome(string s, int left, int right)
    {
        if(s.empty())
            return true;
        while(left < right)
        {
            if(s[left++] != s[right--])
                return false;
        }
        return true;
    }
    bool validPalindrome(string s) {
        int left = 0;
        int right = s.size() - 1;
        while(left < right)
        {
            if(s[left] != s[right])
                return isPalindrome(s, left, right - 1) || isPalindrome(s, left + 1, right);
            left++;
            right--;
        }
        return true;
    }
};
```

## **合并两个有序数组**

[Leetcode：88 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/submissions/)

**题目描述**

给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

```html
Input: nums1 = [1,2,3,0,0,0], m = 3
 		  nums2 = [2,5,6],       n = 3
Output: [1,2,2,3,5,6]
```
```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int index1 = m - 1, index2 = n - 1;
        int indexMerge = m + n - 1;
        while (index1 >= 0 || index2 >= 0) {
            //nums1 为空
            if (index1 < 0)
            {
                nums1[indexMerge] = nums2[index2];
                indexMerge--;
                index2--;
            }
            //nums2 为空
            else if (index2 < 0)
            {
                nums1[indexMerge] = nums1[index1];
                indexMerge--;
                index1--;
            }
            //nums1 元素大于 nums2 
            else if (nums1[index1] > nums2[index2])
            {
                nums1[indexMerge] = nums1[index1];
                indexMerge--;
                index1--;
            }
            //nums1 元素小于 nums2
            else
            {
                nums1[indexMerge] = nums2[index2];
                indexMerge--;
                index2--;
            }
        }
    }
};
```
## **环形链表**


[Leetcode：141 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)


**题目描述**

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

```html
Input：head = [3,2,0,-4], pos = 1
Output：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        //链表为空
        if(head == NULL)
            return false;
        ListNode* slow = head;  //定义快指针
        ListNode* fast = slow->next;    //定义慢指针
        while(slow != NULL && fast != NULL && fast->next != NULL)
        {
            if(slow == fast)
                return true;
            slow = slow->next;
            fast = fast->next->next;
        }
        return false;
    }
};
```
## **最长子序列**

[Leetcode：524 最长子序列](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)


----------
**题目描述**

给定一个字符串和一个字符串字典，找到字典里面最长的字符串，该字符串可以通过删除给定字符串的某些字符来得到。如果答案不止一个，返回长度最长且字典顺序最小的字符串。如果答案不存在，则返回空字符串。

```html
Input: s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: "apple"
```

```c++
class Solution {
public:
    bool isValid(string s, string target)
    {
        int i = 0, j = 0;
        while(i < s.size() && j < target.size())
        {
            if(s[i] == target[j])
                j++;
            i++;
        }
        return j == target.size();
    }
    
    
    string findLongestWord(string s, vector<string>& d) {
        string longestWord = "";
    for (auto& target : d) {
        int max_len = longestWord.size(), len = target.size();
        if (max_len > len || (max_len == len && longestWord.compare(target) < 0)) {
            continue;
        }
        if (isValid(s, target)) {
            longestWord = target;
        }
    }
    return longestWord;
    }
};
```

## **倒数第 K 大元素**

[Leetcode 215：数组的第 K 大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)


----------

**题目描述**

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

```html
Input: [3,2,1,5,6,4] 和 k = 2
Output: 5
```

```c++
struct cmp
{
    bool operator()(int x, int y)
    {
        return x > y;
    }
};
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        /*
        priority_queue<int> q;
        for(auto val : nums)
        {
            q.push(val);
            if(q.size() > nums.size() - k + 1)
                q.pop();
        }
        return q.top();
        */
        priority_queue<int, vector<int>, cmp> q;
        for(auto val : nums)
        {
            q.push(val);
            if(q.size() > k)
                q.pop();
        }
        return q.top();
    }
};
```

## **分发饼干**


----------


[Leetcode：455 分发饼干](https://leetcode-cn.com/problems/assign-cookies/)

**题目描述**

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。对每个孩子 i ，都有一个胃口值 gi ，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j ，都有一个尺寸 sj 。如果 sj >= gi ，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

注意：

你可以假设胃口值为正。
一个小朋友最多只能拥有一块饼干。

```html
Input: [1,2,3], [1,1]

Output: 1
```

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int gi = 0, si = 0;
        //gi    胃口， si  尺寸
        while(gi < g.size() && si < s.size())
        {
            if(s[si] >= g[gi])  //如果 si >= gi；孩子便会得到满足
                gi++;
            si++;   //否则饼干尺寸++
        }
        return gi;
    }
};
```

## **无重叠区间**

[Leetcode：435 无重叠区间](https://leetcode-cn.com/problems/non-overlapping-intervals/)


**题目描述**

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

注意:

可以认为区间的终点总是大于它的起点。
区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

```html
Input: [ [1,2], [2,3], [3,4], [1,3] ]

Output: 1

complex: 移除 [1,3] 后，剩下的区间没有重叠。
```

```c++
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    static bool cmp(const Interval& a, const Interval& b)
    {
        return a.end < b.end;
    }
    int eraseOverlapIntervals(vector<Interval>& intervals) {
        if(intervals.empty())
            return 0;
        int ans = 1;
        sort(intervals.begin(), intervals.end(), cmp);
        int _end = intervals[0].end;
        
        for(int i = 0;i < intervals.size();++i)
        {
            if(intervals[i].start < _end)
            {
                continue;
            }
            _end = intervals[i].end;
            ans++;
        }
        return intervals.size() - ans;
    }
};
```