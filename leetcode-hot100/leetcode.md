# Leetcode算法学习

## 25-10-27：17，78，131

[17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

```
private static final String[] MAPPING = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
```

**示例 1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例 2：**

```
输入：digits = "2"
输出：["a","b","c"]
```

 

**提示：**

- `1 <= digits.length <= 4`
- `digits[i]` 是范围 `['2', '9']` 的一个数字。



**思路：回溯中的子集型问题**

可以画个二叉树，深度为0，可以选a,b,c。深度为1时，可以选择d,e,f。利用path变量存储每一枝叶的字符，当深度到达n时，将path添加到ans中。

**代码：**

```
class Solution {
    private static final String[] MAPPING = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};

    public List<String> letterCombinations(String digits) {
        int n = digits.length();
        List<String> ans = new ArrayList<>();
        char[] path = new char[n];
        dfs(0,ans,path,digits.toCharArray());
        return ans;
    }
    private void dfs(int i, List<String> ans, char[] path, char[] digits) {
        if(i == digits.length){
            ans.add(new String(path));
            return;
        }
         String letters = MAPPING[digits[i] - '0'];
        for (int j = 0; j < letters.length(); j++) {
            path[i] = letters.charAt(j);  // 使用charAt()方法获取字符
            dfs(i + 1, ans, path, digits);
        }
    }
}
```

[78. 子集](https://leetcode.cn/problems/subsets/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给你一个整数数组 `nums` ，数组中的元素 **互不相同** 。返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。你可以按 **任意顺序** 返回解集。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**示例 2：**

```
输入：nums = [0]
输出：[[],[0]]
```

 

**提示：**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- `nums` 中的所有元素 **互不相同**

**思路：回溯中的子集型问题**

每一层我们都可以选择添加或者不添加当前元素，所以说二叉树的深度与nums的长度一致。进行递归后，再将path的最后一个元素删除，回复现场。

```
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        dfs(0, nums, path, ans);
        return ans;
    }
    private void dfs(int i,int[] nums, List<Integer> path, List<List<Integer>> ans) {
        if(i == nums.length){
            ans.add(new ArrayList<Integer>(path));
            return;
        }
        // 不选择当前元素
        dfs(i + 1, nums, path, ans);
        
        // 选择当前元素
        path.add(nums[i]);
        dfs(i + 1, nums, path, ans);
        //回溯
        path.removeLast();
    }       
}
```





[131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给你一个字符串 `s`，请你将 `s` 分割成一些 子串，使每个子串都是 **回文串** 。返回 `s` 所有可能的分割方案。

 

**示例 1：**

```
输入：s = "aab"
输出：[["a","a","b"],["aa","b"]]
```

**示例 2：**

```
输入：s = "a"
输出：[["a"]]
```

 

**提示：**

- `1 <= s.length <= 16`
- `s` 仅由小写英文字母组成

**思路：回溯中的子集型问题**

将字符串s可以看成如（“a,a,c”),选着是否用逗号分割字符串，如果分割的子字符是回文的着选择分割，可选择分割的字符次数取决逗号的个数。

```
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> ans = new ArrayList<>();
        List<String> path = new ArrayList<>();
        dfs(0,0,s,path,ans);
        return ans;
    }
    public void dfs(int i,int start,String s,List<String> path,List<List<String>> ans) {
        if(i == s.length()){
            ans.add(new ArrayList<String>(path));
            return;
        }
        //不分割
        if(i < s.length() - 1){
            dfs(i+1,start,s,path,ans);
        }
        //分割
        if(isPalindrome(s,start,i)) {
            path.add(s.substring(start, i+1));
            dfs(i+1,i+1,s,path,ans);
            path.removeLast();
        }

    }
    public boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left++) != s.charAt(right--)) {
                return false;
            }
        }
        return true;
    }
}
```

## 25-10-29：77，216，22

[77. 组合](https://leetcode.cn/problems/combinations/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

 

**示例 1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**示例 2：**

```
输入：n = 1, k = 1
输出：[[1]]
```

**思路：回溯中的组合型问题**

倒叙枚举

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<Integer> path = new ArrayList<>();
        List<List<Integer>> ans = new ArrayList<>();
        dfs(n,n,k,path,ans);//倒序枚举
        return ans;
    }
    public void dfs(int i,int n,int k,List<Integer> path,List<List<Integer>> ans) {
        int d = k - path.size();
        if (path.size() == k) {
            ans.add(new ArrayList(path));
            return;
        }
        for(int j = i;j >= d;j--){
            path.add(j);
            dfs(j-1,n,k,path,ans);
            path.removeLast();
        }
    }
}
```

选和不选，当path的长度等于k是记录答案，当path的长度+(n - i + 1) < k 时停止

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<Integer> path = new ArrayList<>();
        List<List<Integer>> ans = new ArrayList<>();
        dfs(1,n,k,path,ans);
        return ans;
    }
    public void dfs(int i,int n,int k,List<Integer> path,List<List<Integer>> ans) {
        if(path.size() == k) {
            ans.add(new ArrayList(path));
            return;
        }
        if (path.size() + (n - i + 1) < k) {//表示递归的边界
            return;
        }
        path.add(i);
        dfs(i+1,n,k,path,ans);
        path.removeLast();
        dfs(i + 1, n, k,path,ans);
    }
}
```

[216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



找出所有相加之和为 `n` 的 `k` 个数的组合，且满足下列条件：

- 只使用数字1到9
- 每个数字 **最多使用一次** 

返回 *所有可能的有效组合的列表* 。该列表不能包含相同的组合两次，组合可以以任何顺序返回。

 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
解释:
1 + 2 + 4 = 7
没有其他符合的组合了。
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
解释:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
没有其他符合的组合了。
```

**示例 3:**

```
输入: k = 4, n = 1
输出: []
解释: 不存在有效的组合。
在[1,9]范围内使用4个不同的数字，我们可以得到的最小和是1+2+3+4 = 10，因为10 > 1，没有有效的组合。
```

 

**提示:**

- `2 <= k <= 9`
- `1 <= n <= 60`

**思路：回溯中的组合型问题**

思考剪枝的条件，当path的长度+9-i+1<k时，或n减不够即path的长度大于k时或者n减多了，或者i枚举超过了9。当path的长度等于k时且n的结果为0时记录path的结果。

```
class Solution {
    private List<List<Integer>> ans = new ArrayList<>();
    private List<Integer> path = new ArrayList<>();
    
    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(1, k, n);
        return ans;
    }
    
    private void dfs(int i, int k, int n) {
        // 如果当前数字超过9，返回
        if (i > 9) {
            return;
        }
        
        // 找到符合条件的组合
        if (path.size() == k && n == 0) {
            ans.add(new ArrayList<>(path));
            return;
        }
        
        // 剪枝：如果路径长度已经超过k，或者n小于0，或者剩余数字不够凑齐k个
        if (path.size() > k || n < 0 || path.size() + (9 - i + 1) < k) {
            return;
        }
        
        // 选择当前数字
        path.add(i);
        dfs(i + 1, k, n - i);
        path.remove(path.size() - 1); // 回溯
        
        // 不选择当前数字
        dfs(i + 1, k, n);
    }
}
```

[22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



数字 `n` 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

 

**示例 1：**

```
输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
```

**示例 2：**

```
输入：n = 1
输出：["()"]
```

 

**提示：**

- `1 <= n <= 8`

**思路：回溯中的组合型问题**

可以知道只有生成了左括号才能生成右括号，即左括号要大于右括号，然后左括号要小于n，i为递归深度，i-open即为右括号数，当path枝叶的长度为2*n时记录答案。

```
class Solution {
    public List<String> ans = new ArrayList<String>();
    public StringBuilder path = new StringBuilder();
    public List<String> generateParenthesis(int n) {
        dfs(0,0,n);
        return ans;
    }
    public void dfs(int i,int open,int n){
        if(path.length() == n * 2){
            ans.add(path.toString());
        }
        if(open < n){
            path.append('(');
            dfs(i+1,open+1,n);
            path.deleteCharAt(path.length() - 1);
        }
        if(i- open < open){
            path.append(')');
            dfs(i+1,open,n);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```

## 25-11-18：198

[198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **不触动警报装置的情况下** ，一夜之内能够偷窃到的最高金额。

 

**示例 1：**

```
输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 2：**

```
输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
```

 

**提示：**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

**思路1**：从选和不选的角度思考

首先肯定是从最后或最前的元素思考，因为它们的约束最少，从最后的元素思考，不选择该元素，那么从剩下的k-1个元素中选择，选择该元素，则从剩下的k-2的元素中选择，那么结果res=max(dfs(k-1),dfs(k-2)+nums[i]),当k=0时结束递归；但这样，会超出时间，可以知道的是在dfs(k-1)这个递归中，他又会算一遍dfs(k-2),所以我们可以用一个cache数值存储该次计算的结果

```
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        cache = [-1] * n
        def dfs(i):
            if i < 0:
                return 0
            if cache[i] != -1:
                return cache[i]
            res = max(dfs(i-1),dfs(i-2)+nums[i])
            cache[i] = res
            return res
        return dfs(n-1)
        
```

**思路2**：从迭代的角度

可以知道的当为k=i时，f[i] = max(f[i-1],f[i-2]+nums[i]),但这样i=0,1时会超出数组空间，改为f[i+2] = max(f[i+1],f[i]+num[i]) 

```
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        f = [0] * (n+2)
        for i, x in enumerate(nums):
            f[i+2] = max(f[i+1],f[i]+nums[i])
        return f[n+1]
```

当然我们还可以进行空间优化，就像斐波那契数组一样，用f0存储上上个数值,f1存储上个数值,f2存储当前的数值

```
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        f0 = f1 = 0
        for i, x in enumerate(nums):
            f2 = max(f1,f0+nums[i])
            f0 = f1
            f1 = f2
        return f2
```

## 25-11-19&20：494

[494. 目标和](https://leetcode.cn/problems/target-sum/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给你一个非负整数数组 `nums` 和一个整数 `target` 。

向数组中的每个整数前添加 `'+'` 或 `'-'` ，然后串联起所有整数，可以构造一个 **表达式** ：

- 例如，`nums = [2, 1]` ，可以在 `2` 之前添加 `'+'` ，在 `1` 之前添加 `'-'` ，然后串联起来得到表达式 `"+2-1"` 。

返回可以通过上述方法构造的、运算结果等于 `target` 的不同 **表达式** 的数目。

 

**示例 1：**

```
输入：nums = [1,1,1,1,1], target = 3
输出：5
解释：一共有 5 种方法让最终目标和为 3 。
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**示例 2：**

```
输入：nums = [1], target = 1
输出：1
```

 

**提示：**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

**思路**：从选和不选的角度

这道题是0/1背包的变形，我们可以用p表示所以正数之和，s为所以数之和，那么所以负数之和s-p，故taget=p-(s-p)；p = (taget+s) // 2,那么p不为负数，且是偶数。

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target += sum(nums)
        if target < 0 or target % 2 != 0:
            return 0
        target //= 2 

        n=len(nums)
        @cache
        def dfs(i, c):
            if i < 0:
                return 1 if c == 0 else 0
            if c < nums[i]:
                return dfs(i-1,c)
            return dfs(i-1,c) + dfs(i-1,c-nums[i])
        return dfs(n-1,target)
```

**思路**：记忆优化

将dfs(i,c)=dfs(i-1,c)+dfs(i-1,c-nums[i])改为数组形式`f[i][c]=f[i-1][c]+f[i-1][c-nums[i]]`也可使是`f[i+1][c]=f[i][c]+f[i][c-nums[i]]`

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target += sum(nums)
        if target < 0 or target % 2 != 0:
            return 0
        target //= 2 

        n = len(nums)

        f = [[0] * (target + 1) for _ in range(n+1)]
        f[0][0] = 1

        for i,x in enumerate(nums):
            for c in range(target+1):
                if c < x:
                    f[i+1][c]=f[i][c]
                else:
                    f[i+1][c]=f[i][c]+f[i][c-nums[i]]
        return f[n][target]
```

可以知道是每次利用两组数值记录数据，分别是这一次和上一次的数组，故可以申请长度为2的f[c]数组，`f[(1+1)%2]=f[i%2][c]+f[i%2][c-nums[i]]`

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target += sum(nums)
        if target < 0 or target % 2 != 0:
            return 0
        target //= 2 

        n = len(nums)

        f = [[0] * (target+1) for _ in range(2)]
        f[0][0] = 1

        for i,x in enumerate(nums):
            for c in range(target+1):
                if c < x:
                    f[(i+1)%2][c]=f[i%2][c]
                else:
                    f[(i+1)%2][c]=f[i%2][c]+f[i%2][c-nums[i]]
        return f[n%2][target]
```

![image-20251120191322348](C:\Users\11695\AppData\Roaming\Typora\typora-user-images\image-20251120191322348.png)

正着枚举计算可以知道会覆盖掉f[2]，如果反着枚举就不会出现这种情况

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target += sum(nums)
        if target < 0 or target % 2 != 0:
            return 0
        target //= 2 

        n = len(nums)

        f = [0] * (target+1)
        f[0] = 1

        for x in nums:
            for c in range(target,x-1,-1):
                f[c] = f[c] + f[c-x]
        return f[target]
```

## 25-11-26：332

[322. 零钱兑换](https://leetcode.cn/problems/coin-change/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给你一个整数数组 `coins` ，表示不同面额的硬币；以及一个整数 `amount` ，表示总金额。

计算并返回可以凑成总金额所需的 **最少的硬币个数** 。如果没有任何一种硬币组合能组成总金额，返回 `-1` 。

你可以认为每种硬币的数量是无限的。

 

**示例 1：**

```
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
```

**示例 2：**

```
输入：coins = [2], amount = 3
输出：-1
```

**示例 3：**

```
输入：coins = [1], amount = 0
输出：0
```

 

**提示：**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`

**思路：从递归的角度**

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        n = len(coins)
        
        @cache
        def dfs(i,c):
            if i < 0:
                return 0 if c==0 else inf;
            if c < coins[i]:
                return dfs(i-1,c)
            return min(dfs(i-1,c),dfs(i,c-coins[i])+1)
        ans = dfs(n-1,amount)
        return ans if ans < inf else -1
```

**思路：从迭代的角度**

`f[i][c]=min(f[i-1][c],f[i][c-conins[i]]+1)`,也就是`f[i+1][c]=min(f[i][c],f[i+1][c-conins[i]+1])`

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        n = len(coins)
        
        f = [[inf] * (amount+1) for _ in range(n+1)]
        f[0][0] = 0

        for i,x in enumerate(coins):
            for c in range(amount+1):
                if c < x:
                    f[i+1][c] = f[i][c]
                else:
                    f[i+1][c]=min(f[i][c],f[i+1][c-x]+1)
        ans = f[n][amount]
        return ans if ans < inf else -1
```

如果正序枚举的话，不会影响最后的数据

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        n = len(coins)
        
        f = [inf] * (amount+1)
        f[0] = 0

        for x in coins:
            for c in range(x,amount+1):
                f[c]=min(f[c],f[c-x]+1)
        ans = f[amount]
        return ans if ans < inf else -1
```

## 25-11-27：1143

[1143. 最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



提示



给定两个字符串 `text1` 和 `text2`，返回这两个字符串的最长 **公共子序列** 的长度。如果不存在 **公共子序列** ，返回 `0` 。

一个字符串的 **子序列** 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。

- 例如，`"ace"` 是 `"abcde"` 的子序列，但 `"aec"` 不是 `"abcde"` 的子序列。

两个字符串的 **公共子序列** 是这两个字符串所共同拥有的子序列。

 

**示例 1：**

```
输入：text1 = "abcde", text2 = "ace" 
输出：3  
解释：最长公共子序列是 "ace" ，它的长度为 3 。
```

**示例 2：**

```
输入：text1 = "abc", text2 = "abc"
输出：3
解释：最长公共子序列是 "abc" ，它的长度为 3 。
```

**示例 3：**

```
输入：text1 = "abc", text2 = "def"
输出：0
解释：两个字符串没有公共子序列，返回 0 。
```

 

**提示：**

- `1 <= text1.length, text2.length <= 1000`
- `text1` 和 `text2` 仅由小写英文字符组成。

**思路：从选或者不选的角度**：

```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m = len(text1)
        n = len(text2)

        @cache
        def dfs(i,j):
            if i < 0 or j < 0:
                return 0
            if text1[i] == text2[j]:
                return dfs(i-1,j-1)+1
            return max(dfs(i-1,j),dfs(i,j-1))
        return dfs(m-1,n-1)
```

翻译成迭代

```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n = len(text1)
        m = len(text2)

        f = [[0]*(m+1) for _ in range(n+1)]

        for i,x in enumerate(text1):
            for j,y in enumerate(text2):
                if x == y:
                    f[i+1][j+1] = f[i][j] +1
                else:
                    f[i+1][j+1] = max(f[i][j+1],f[i+1][j])
        return f[n][m]
```

![image-20251127210854408](C:\Users\11695\AppData\Roaming\Typora\typora-user-images\image-20251127210854408.png)

利用pre存储当前变量

```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n = len(text1)
        m = len(text2)

        f = [0]*(m+1)

        for i,x in enumerate(text1):
            pre = f[0]
            for j,y in enumerate(text2):
                tmp = f[j+1]
                if x == y:
                    f[j+1] = pre +1
                else:
                    f[j+1] = max(f[j+1],f[j])
                pre = tmp
        return f[m]
```

## 25-12-2：72

[72. 编辑距离](https://leetcode.cn/problems/edit-distance/)

已解答

中等



相关标签

![premium lock icon](https://static.leetcode.cn/cn-frontendx-assets/production/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)相关企业



给你两个单词 `word1` 和 `word2`， *请返回将 `word1` 转换成 `word2` 所使用的最少操作数* 。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

 

**示例 1：**

```
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**示例 2：**

```
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```

**思路：递归**

```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        n = len(word1)
        m = len(word2)
        
        @cache  
        def dfs(i, j):          
            # 边界情况1：如果word1已处理完（i < 0）
            # 则需要插入word2[0..j]的所有字符，操作数为j+1
            if i < 0:
                return j + 1                
            # 边界情况2：如果word2已处理完（j < 0）
            # 则需要删除word1[0..i]的所有字符，操作数为i+1
            if j < 0:
                return i + 1
                
            # 情况1：当前字符匹配
            # 如果word1[i] == word2[j]，则不需要操作
            # 直接递归处理前一个字符：dfs(i-1, j-1)
            if word1[i] == word2[j]:
                return dfs(i-1, j-1)
                
            # 情况2：当前字符不匹配
            # 需要选择三种操作中的最小值，然后加1（表示本次操作）
            # 1. dfs(i-1, j) + 1: 删除word1[i]字符
            # 2. dfs(i, j-1) + 1: 在word1中插入word2[j]字符
            # 3. dfs(i-1, j-1) + 1: 将word1[i]替换为word2[j]
            return min(dfs(i-1, j), dfs(i, j-1), dfs(i-1, j-1)) + 1
        
        # 从两个字符串的末尾开始递归计算
        # 初始调用：计算将整个word1转换为整个word2的最小编辑距离
        return dfs(n-1, m-1)
```

翻译成迭代

```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        n = len(word1)
        m = len(word2)

        f = [[0]*(m+1) for _ in range(n+1)]
        f[0] = list(range(m+1))
        for i,x in enumerate(word1):
            f[i+1][0] = i+1
            for j,y in enumerate(word2):
                if x == y:
                    f[i+1][j+1] = f[i][j]
                else:
                    f[i+1][j+1] = min(f[i][j+1],f[i+1][j],f[i][j])+1
        return f[n][m]

```

