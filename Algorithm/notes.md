# 24. Swap Nodes in Pairs

## 题目

Given a linked list, swap every two adjacent nodes and return its head.  You must solve the problem without modifying the values in the list's  nodes (i.e., only nodes themselves may be changed.)

**Example:**

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

## 题目大意

将两两相邻的节点相互交换

## 思路

一开始想的就是建立`pre`和`cur`指针，同时建立一个临时变量`a = cur->next`，使得`cur`指向`a->next`，`a`指向`cur`，`pre`又指向`a`，思路是对的，就是实现得有点复杂，导致时间是53.17%，空间是6.97%，代码如下：

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* p = head;
        ListNode* pre = head;
        while(p && p->next){
            ListNode* a = p->next;
            p->next = a->next;
            a->next = p;
            if(p == head){
                head = a;
            }else{
                pre->next = a;
            }
            pre = p;
            p = p->next;
        }
        return head;
    }
};
```

## 代码

后来有幸看到几个大佬的做法，修改了一下。

代码一：

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* res = new ListNode();
        ListNode* pre = res;
        ListNode* cur = head;
        while(cur && cur->next){
            pre->next = cur->next;
            cur->next = pre->next->next;
            pre->next->next = cur;
            pre = cur;
            cur = cur->next;
        }
        return res->next;
    }
};
```

代码二：这是一种递归的做法，代码非常简洁，用时跟上面的差不多。

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* tmp = head->next;
        head->next = swapPairs(tmp->next);
        tmp->next = head;
        return tmp;
    }
};
```

#  7. Reverse Integer

## 题目

Given a signed 32-bit integer `x`, return `x` *with its digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-231, 231 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example1:**

```
Input: x = 123
Output: 321
```



**Example2:**

```
Input: x = -123
Output: -321
```

## 题目大意

将数字倒过来，**但是假设环境中不能存储 64位的整数**。

## 思路

不能存储64位的整数就意味着不能开`long`、`long long`之类的，所以题目的难点在于怎么处理数字的边界问题，也就是程序中的任何一个变量都不能超过32位整数范围，得先进行预判。

本来想着用

```c++
if(res * 10 + x % 10 < 0 && !sign ||res * 10 + x % 10 > 0 && sign) return 0;
```

这个公式来处理越界的问题，但是`res * 10 + x % 10`这个已经越界了，所以没办法处理，只能考虑将`res`变小，而且不知道`int`的最大值可以用`INT_MAX`表示，最小值用`INT_MIN`表示。

## 代码

```c++
class Solution {
public:
    int reverse(int x) {
        int res = 0;
        while(x){
            int k = x % 10;
            if(res > INT_MAX / 10 || res == INT_MAX / 10 && k > 7) return 0;
            if(res < INT_MIN / 10 || res == INT_MIN / 10 && k < -8) return 0;
            res = res * 10 + k;
            x /= 10;
        }
        return res;
    }
};
```

# 8. String to Integer (atoi)

## 题目

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).

The algorithm for `myAtoi(string s)` is as follows:

1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is `'-'` or `'+'`. Read this character in if it is either. This determines if the final  result is negative or positive respectively. Assume the result is  positive if neither is present.
3. Read in next the characters until the next non-digit character or  the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. `"123" -> 123`, `"0032" -> 32`). If no digits were read, then the integer is `0`. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range `[-2^31, 2^31 - 1]`, then clamp the integer so that it remains in the range. Specifically, integers less than `-231` should be clamped to `-2^31`, and integers greater than `2^31 - 1` should be clamped to `2^31 - 1`.
6. Return the integer as the final result.

**Note:**

- Only the space character `' '` is considered a whitespace character.
- **Do not ignore** any characters other than the leading whitespace or the rest of the string after the digits.

 

**Example 1:**

```
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-2^31, 2^31 - 1], the final result is 42.
```

**Example 2:**

```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-2^31, 2^31 - 1], the final result is -42.
```

**Example 3:**

```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-2^31, 2^31 - 1], the final result is 4193.
```

## 题目大意

将字符串里的数字转换为32位整数，超出范围的需要截断到边界值。

## 思路

无非就是简单的字符串处理，按照步骤来就好，不过写的有点复杂，时间为77.17%。

```c++
class Solution {
public:
    int myAtoi(string s) {
        bool sign = false, first = true;
        int ans = 0;
        
        for(int i = 0; i < s.size(); i++){
            if(s[i] == ' '){
                if(first) continue;
                else break;
            }else if(s[i] == '+'){
                if(first) first = false;
                else break;
            }else if(s[i] == '-'){
                if(first){
                    sign = true;
                    first = false;
                }else break;
            }else if(isdigit(s[i])){
                if(first) first = false;
                int k = s[i] - '0';
                k = sign ? -k : k;
                if(ans > INT_MAX / 10 || ans == INT_MAX / 10 && k > 7) return INT_MAX;
                if(ans < INT_MIN / 10 || ans == INT_MIN / 10 && k < -8) return INT_MIN;
                ans = ans * 10 + k;
            }else break;
        }
        
        return ans;
        
    }
};
```

## 代码

看了官方的解答，果然速度快了，100%了（后来发现这个速度就是玄学）。

```c++
class Solution {
public:
    int myAtoi(string input) {
        int sign = 1; 
        int result = 0; 
        int index = 0;
        int n = input.size();
        
        // Discard all spaces from the beginning of the input string.
        while (index < n && input[index] == ' ') { 
            index++; 
        }
        
        // sign = +1, if it's positive number, otherwise sign = -1. 
        if (index < n && input[index] == '+') {
            sign = 1;
            index++;
        } else if (index < n && input[index] == '-') {
            sign = -1;
            index++;
        }
        
        // Traverse next digits of input and stop if it is not a digit. 
        // End of string is also non-digit character.
        while (index < n && isdigit(input[index])) {
            int digit = input[index] - '0';

            // Check overflow and underflow conditions. 
            if ((result > INT_MAX / 10) || (result == INT_MAX / 10 && digit > INT_MAX % 10)) { 
                // If integer overflowed return 2^31-1, otherwise if underflowed return -2^31.    
                return sign == 1 ? INT_MAX : INT_MIN;
            }
            
            // Append current digit to the result.
            result = 10 * result + digit;
            index++;
        }
        
        // We have formed a valid number without any overflow/underflow.
        // Return it after multiplying it with its sign.
        return sign * result;
    }
};
```

# 29. Divide Two Integers

## 题目

Given two integers `dividend` and `divisor`, divide two integers **without** using multiplication, division, and mod operator.

The integer division should truncate toward zero, which means losing its fractional part. For example, `8.345` would be truncated to `8`, and `-2.7335` would be truncated to `-2`.

Return *the **quotient** after dividing* `dividend` *by* `divisor`.

**Note:** Assume we are dealing with an environment that could only store integers within the **32-bit** signed integer range: `[−2^31, 2^31 − 1]`. For this problem, if the quotient is **strictly greater than** `2^31 - 1`, then return `2^31 - 1`, and if the quotient is **strictly less than** `-2^31`, then return `-2^31`.

 

**Example 1:**

```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = 3.33333.. which is truncated to 3.
```

**Example 2:**

```
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = -2.33333.. which is truncated to -2.
```

## 题目大意

被除数除以除数，求商，但不能进行除法、乘法和求余运算，得到的结果取整数部分，而且整个环境只能存储32位有符号整数。

## 思路

一开始想着用减法，但是如果被除数太大，除数太小，就会TLE，所以我们要把除数变大，再用减法，把除数变大的方法就是用位左移，使得除数最接近被除数。

## 代码

```c++
class Solution {
public:
    int divide(int dividend, int divisor) {
        if(dividend == 0) return 0;
        
        if(divisor == INT_MIN) return dividend == INT_MIN ? 1 : 0;
        
        int neg = (dividend > 0) ^ (divisor > 0);
        
        // Here is different from the description above.
		// In practice, we force our dividend to be negative.
		// Because the range of negative values (2^31) is larger than the range of positive values (2^31 - 1).
		// If we force dividend to be positive, there may be integer overflow.
        if(dividend > 0) dividend = 0 - dividend;
        
		// Divisor should be positive.
		// Because we will apply bitwise shift to it.
		// And we have handled the case when divisor is INT_MIN.
        if(divisor < 0) divisor = 0 - divisor;
        
        int ans = 0;
        
        while(dividend <= -divisor){
            int tmp = divisor, step = 1;
            
            while(tmp < 1<<30 && -tmp >= dividend){
                tmp <<= 1;
                step <<= 1;
            }
            
            if(-tmp < dividend){
                tmp >>= 1;
                step >>= 1;
            }
            
            dividend += tmp;
            ans -= step;
        }
        
        if(neg) return ans;
        else return ans == INT_MIN ? INT_MAX : -ans;
    }
};
```

# 36. Valid Sudoku

## 题目

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

 

**Example 1:**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

## 题目大意

根据数独的规则判断一个数独是否成立。

## 思路

按照规则写判断函数建立几个数组去存储，避免重复判断。

## 代码

```c++
class Solution {
public:
    bool block[3][3] = {false};
    bool row[9] = {false};
    bool col[9] = {false};
    
    bool validBlock(vector<vector<char>>& board, int r, int c){
        int rr = r / 3, cc = c / 3;
        int cnt[10] = {0};
        for(int i = rr * 3; i < (rr + 1) * 3; i++){
            for(int j = cc * 3; j < (cc + 1) * 3; j++){
                if(board[i][j] == '.') continue;
                if(cnt[board[i][j] - '0']) return false;
                cnt[board[i][j] - '0']++;
            }
        }
        return true;
    }
    
    bool validRow(vector<vector<char>>& board, int r){
        int cnt[10] = {0};
        for(int i = 0; i < 9; i++){
            if(board[r][i] == '.') continue;
            if(cnt[board[r][i] - '0']) return false;
            cnt[board[r][i] - '0']++;
        }
        return true;
    }
    
    bool validCol(vector<vector<char>>& board, int c){
        int cnt[10] = {0};
        for(int i = 0; i < 9; i++){
            if(board[i][c] == '.') continue;
            if(cnt[board[i][c] - '0']) return false;
            cnt[board[i][c] - '0']++;
        }
        return true;
    }
    
    bool isValidSudoku(vector<vector<char>>& board) {
        for(int r = 0; r < 9; r++){
            for(int c = 0; c < 9; c++){
                if(board[r][c] == '.') continue;
                if(!block[r/3][c/3]){
                    bool flag = validBlock(board, r, c);
                    if(!flag) return false;
                    block[r/3][c/3] = true;
                }
                if(!row[r]){
                    bool flag = validRow(board, r);
                    if(!flag) return false;
                    row[r] = true;
                }
                if(!col[c]){
                    bool flag = validCol(board, c);
                    if(!flag) return false;
                    col[c] = true;
                }
            }
        }
        return true;
    }
};
```

# 38. Count and Say

## 题目

The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the way you would "say" the digit string from `countAndSay(n-1)`, which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the **minimal** number of groups so that each group is a contiguous section all of the **same character.** Then for each group, say the number of characters, then say the  character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

For example, the saying and conversion for digit string `"3322251"`:

![img](https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg)

Given a positive integer `n`, return *the* `nth` *term of the **count-and-say** sequence*.

 

**Example 1:**

```
Input: n = 1
Output: "1"
Explanation: This is the base case.
```

**Example 2:**

```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

## 题目大意

像一种递归的形式，将n-1对应的字符串说出来。

## 思路

写一个递归，出口条件是当`n = 1`时，返回`"1"`；获取`n - 1`时的字符串，然后循环遍历将其说出来。

## 代码

```c++
class Solution {
public:
    string countAndSay(int n) {
        if(n == 1) return "1";
        string pre = countAndSay(n - 1);
        
        int cnt = 1, x = pre[0] - '0';
        string ans = "";
        
        for(int i = 1; i < pre.size(); i++){
            if(pre[i] != pre[i-1]){
                ans += cnt + '0';
                ans += x + '0';
                cnt = 1;
                x = pre[i] - '0';
            }else{
                cnt++;
            }
        }
        
        ans += cnt + '0';
        ans += x + '0';
        
        return ans;
    }
};
```

# 50. Pow(x, n)

## 题目

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `x^n`).

 

**Example 1:**

```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

**Example 2:**

```
Input: x = 2.10000, n = 3
Output: 9.26100
```

**Example 3:**

```
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2^(-2) = 1/2^2 = 1/4 = 0.25
```

## 题目大意

求`x`的`n`次幂

## 思路

这个要是直接乘会TLE，所以我们用到了快速幂的方法（直接套模板），注意处理边界问题。

## 代码

```c++
class Solution {
public:
    double myPow(double x, int n) {
        double res = 1.0;
        bool neg = false;
        if(n == INT_MIN){
            x *= x;
            n = 1 << 30;
            neg = true;
        }else if(n < 0){
            n = 0 - n;
            neg = true;
        }
        while(n){
            if(n & 1){
                res *= x;
            }
            x *= x;
            n >>= 1;
        }
        return neg ? 1.0 / res : res;
    }
};
```

# 503. Next Greater Element II

## 题目

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return *the **next greater number** for every element in* `nums`.

The **next greater number** of a number `x`  is the first greater number to its traversing-order next in the array,  which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

 

**Example 1:**

```
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.
```

**Example 2:**

```
Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
```

## 题目大意

求每个元素下一个比它更大的元素。

## 思路

一开始想着用队列和栈实现，顺序遍历，队列顺序存着从小到大的数，栈顺序存着从大到小的数：

```c++
class Solution {
public:
    int ans[10005];
    int q[10005];
    int stk[10005];
    int hh = 0, tt = -1, top = -1;
    vector<int> nextGreaterElements(vector<int>& nums) {
        vector<int> res;
        q[++tt] = 0;
        stk[++top] = 0;
        for(int i = 1; i < nums.size(); i++){
            while(top != -1 && nums[i] > nums[stk[top]]){
                int k = stk[top--];
                ans[k] = i;
            }
            stk[++top] = i;
            if(nums[i] > nums[q[tt]]){
                q[++tt] = i;
            }
        }
        
        while(top != -1){
            int k = stk[top--];
            while(hh <= tt && nums[q[hh]] <= nums[k]) hh++;
            if(hh > tt){
                ans[k] = -1;
            }else{
                ans[k] = q[hh];
            }
        }
        
        for(int i = 0; i < nums.size(); i++){
            if(ans[i] != -1){
                res.push_back(nums[ans[i]]);
            }else{
                res.push_back(-1);
            }
        }
        
        return res;
    }
};
```

结果还不错，不过有些复杂

## 代码

看了官方解答，代码简洁了不少

```c++
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> s;
        int n = nums.size();
        vector<int> res(n, -1);
        
        for(int i = 2 * n - 1; i >= 0; i--){
            while(!s.empty() && nums[i%n] >= s.top()) s.pop();
            if(i < n && !s.empty() && nums[i] < s.top()) res[i] = s.top();
            s.push(nums[i%n]);
        }
        
        return res;
    }
};
```

# 54. Spiral Matrix

## 题目

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## 题目大意

将矩阵中的元素按蛇形顺序打印出来

## 思路

一开始想着一圈一圈由外向里地打印，可能判断条件写得不够好，导致用时长：

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<int> res;
        int cnt = 0;
        
        do{
            for(int i = cnt; i < n + cnt; i++){
                res.push_back(matrix[cnt][i]);
            }
            
            for(int i = cnt + 1; i < m + cnt; i++){
                res.push_back(matrix[i][n+cnt-1]);
            }
            
            for(int i = cnt + n - 2; m >= 2 && i >= cnt; i--){
                res.push_back(matrix[m+cnt-1][i]);
            }
            
            for(int i = m + cnt - 2; n >= 2 && i >= cnt + 1; i--){
                res.push_back(matrix[i][cnt]);
            }
            
            m -= 2;
            n -= 2;
            cnt++;
        }while(m > 0 && n > 0);
        
        return res;
    }
};
```

## 代码

看了一个大佬的代码，感觉比我写的清晰多了，通俗易懂多了，有条理多了，复刻如下：

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        int st_row = 0, ed_row = m - 1, st_col = 0, ed_col = n - 1;
        int cnt = 0, tol = m * n;
        vector<int> res;
        
        while(cnt < tol){
            for(int i = st_col; cnt < tol && i <= ed_col; i++){
                res.push_back(matrix[st_row][i]);
                cnt++;
            }
            st_row++;
            
            for(int i = st_row; cnt < tol && i <= ed_row; i++){
                res.push_back(matrix[i][ed_col]);
                cnt++;
            }
            ed_col--;
            
            for(int i = ed_col; cnt < tol && i >= st_col; i--){
                res.push_back(matrix[ed_row][i]);
                cnt++;
            }
            ed_row--;
            
            for(int i = ed_row; cnt < tol && i >= st_row; i--){
                res.push_back(matrix[i][st_col]);
                cnt++;
            }
            st_col++;
        }
        
        return res;
    }
};
```

# 73. Set Matrix Zeroes

## 题目

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

## 题目大意

一个位置有0，那么这个0所在的行和列全部置为0

## 思路

一开始想的是遍历，到0了就把行列变为0，并标记一下该行/该列已经变为0，同时为了区分原先是0还是后面变为0做了标记，但是时间和空间不理想。后来看了某位大佬的做法，是遍历的时候先不置为0，看到0就把0的坐标放入vector中，最后再遍历一次把他们所在的行和列置为0。

```c++
class Solution {
public:
    bool flag[205][205];
    bool row[205];
    bool col[205];
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j]) continue;
                if(flag[i][j]) continue;
                if(!row[i]){
                    for(int k = 0; k < n; k++){
                        if(!matrix[i][k]) continue;
                        matrix[i][k] = 0;
                        flag[i][k] = true;
                    }
                    row[i] = true;
                }
                if(!col[j]){
                    for(int k = 0; k < m; k++){
                        if(!matrix[k][j]) continue;
                        matrix[k][j] = 0;
                        flag[k][j] = true;
                    }
                    col[j] = true;
                }
            }
        }
    }
};
```

## 代码

```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<pair<int, int>> v;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(!matrix[i][j]) v.push_back(make_pair(i, j));
            }
        }
        
        for(int k = 0; k < v.size(); k++){
            int c = 0, r = 0;
            while(c < n){
                matrix[v[k].first][c] = 0;
                c++;
            }
            
            while(r < m){
                matrix[r][v[k].second] = 0;
                r++;
            }
        }
    }
};
```

# 116. Populating Next Right Pointers in Each Node

## 题目

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2:**

```
Input: root = []
Output: []
```

## 题目大意

用`next`指针指向节点右边第一个节点，如果没有指向`null`

## 思路

用bfs遍历每一层，如果那一层还有剩节点那就指向队头的节点，如果没有就指向null

## 代码

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if(root == nullptr) return nullptr;
        queue<Node*> q;
        q.push(root);
        while(q.size()){
            int cnt = q.size();
            while(cnt){
                Node* tmp = q.front();
                q.pop();
                cnt--;
                if(cnt){
                    tmp->next = q.front();
                }
                if(tmp->left) q.push(tmp->left);
                if(tmp->right) q.push(tmp->right);
            }
            
        }
        return root;
    }
};
```

