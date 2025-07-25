


# LeetCode 热题 100

https://leetcode.cn/studyplan/top-100-liked/



## 哈希




### 49. 字母异位词分组
已解答
中等
相关标签
premium lock icon
相关企业
给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。

 

示例 1:

输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]

输出: [["bat"],["nat","tan"],["ate","eat","tea"]]

解释：

在 strs 中没有字符串可以通过重新排列来形成 "bat"。
字符串 "nat" 和 "tan" 是字母异位词，因为它们可以重新排列以形成彼此。
字符串 "ate" ，"eat" 和 "tea" 是字母异位词，因为它们可以重新排列以形成彼此。

示例 2:

输入: strs = [""]

输出: [[""]]

示例 3:

输入: strs = ["a"]

输出: [["a"]]

 

提示：

1 <= strs.length <= 10^4
0 <= strs[i].length <= 100
strs[i] 仅包含小写字母




#### 代码

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {



        Map<String,List<String>> anagramGroups = new HashMap<>();


        for( String s : strs ) {

            int[] charCounts = new int[26];


            for( char c : s.toCharArray() ) {

                charCounts[c - 'a']++;
            }


            String key = Arrays.toString( charCounts );


            List<String> listForGroup = anagramGroups.getOrDefault( key ,new ArrayList<>());

            listForGroup.add(s);

            anagramGroups.put( key, listForGroup );



        }


        return new ArrayList<>( anagramGroups.values() );
        
    }
}
```




```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:


        anagram_groups = defaultdict(list)

        for s in strs:

            char_counts = [0] * 26

            for char_code in map( ord,s ):

                char_counts[char_code - ord('a')] += 1

            key = tuple( char_counts )

            anagram_groups[key].append(s)

        return list( anagram_groups.values() )
        
        
```





#### 讲解

好的，作为一名高级软件工程师，我将极尽详细地为你讲解 LeetCode 上的“字母异位词分组”这道算法题，并提供详细的 Java 和 Python 代码实现。

---

 1. 理解问题

首先，我们来仔细理解一下题目要求：

*   **输入**: 一个字符串数组 `strs`。
*   **目标**: 将所有**字母异位词**（Anagrams）组合在一起，并以列表的形式返回。
*   **输出格式**: 结果是一个列表的列表，内部子列表的顺序以及子列表内字符串的顺序可以任意。
*   **字母异位词定义**: 两个字符串如果包含完全相同的字符，并且每个字符的**数量也相同**，那么它们就是字母异位词。换句话说，一个字符串可以通过重新排列其字符来形成另一个字符串。
    *   例如："eat", "tea", "ate" 都是字母异位词，因为它们都由一个 'a'，一个 'e'，一个 't' 组成。
*   **约束**:
    *   `strs` 数组的长度在 1 到 10^4 之间。
    *   `strs[i]` 中每个字符串的长度在 0 到 100 之间。
    *   `strs[i]` 仅包含小写英文字母。

**示例分析：**

*   `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`
    *   "eat", "tea", "ate" 是一组异位词。
    *   "tan", "nat" 是一组异位词。
    *   "bat" 独立成组。
    *   输出可以是 `[["bat"],["nat","tan"],["ate","eat","tea"]]` （顺序可能不同）。

*   `strs = [""]`
    *   空字符串本身就是一组。
    *   输出 `[[""]]`。

*   `strs = ["a"]`
    *   单个字符本身就是一组。
    *   输出 `[["a"]]`。

---

 2. 核心思想：如何识别字母异位词？

要将字母异位词组合在一起，关键在于找到一种方法，使得**所有字母异位词都能映射到同一个唯一的“键”**，而其他非异位词则映射到不同的键。

有两种常用的方法来生成这个“键”：

1.  **排序字符法 (Sorting Characters)**:
    *   对于每个字符串，将其字符进行排序，然后将排序后的字符重新组合成一个新字符串。
    *   例如：
        *   "eat" -> 排序后 "aet"
        *   "tea" -> 排序后 "aet"
        *   "ate" -> 排序后 "aet"
    *   这样，所有是字母异位词的字符串都会得到相同的排序后的字符串。这个排序后的字符串就可以作为 HashMap 的键。
    *   优点：概念简单，实现直接。
    *   缺点：对每个字符串进行排序的时间复杂度是 `O(L log L)`，其中 `L` 是字符串的长度。如果字符串很长，这可能会比较慢。

2.  **字符计数法 (Character Counting)**:
    *   对于每个字符串，统计其中每个字符（'a' 到 'z'）出现的频率。
    *   由于字符串只包含小写英文字母，我们可以用一个固定大小的数组（例如 `int[26]`）来存储频率。
    *   例如："eat" -> `{'a': 1, 'e': 1, 't': 1}`。我们可以将这个频率数组转换成一个唯一的字符串作为键，比如 `"#1#0#0#0#1#...#1#0..."` (表示 'a' 出现 1 次，'b' 出现 0 次，'e' 出现 1 次，'t' 出现 1 次，其余为 0)。
    *   优点：统计频率的时间复杂度是 `O(L)`。将频率数组转换为键的时间复杂度是 `O(26)` (常数时间)。因此，总体上比排序法更快。
    *   缺点：实现上可能比直接排序稍微复杂一点点，需要考虑如何将频率数组转换为一个合适的键。

**选择哪种方法？**

考虑到字符串长度 `L` 最大为 100，两种方法在时间上都是可接受的。
*   `N * L log L` (排序法): `10^4 * 100 * log(100) ≈ 10^6 * 7 = 7 * 10^6`
*   `N * L` (字符计数法): `10^4 * 100 = 10^6`

字符计数法在理论上略快，且对于固定字符集的问题，它是一个非常通用的优化技巧。在 Java 中，`Arrays.toString(int[])` 可以方便地将频率数组转换为一个唯一的字符串表示，可以直接用作 HashMap 的键。在 Python 中，`tuple(list)` 可以将列表转换为不可变的元组，也可以直接用作字典的键。

我们将采用**字符计数法**来实现，因为它更通用且效率更高。

---

 3. 核心思想：哈希表 (HashMap / Dictionary) 的应用

一旦我们有了将异位词映射到相同键的方法，就可以使用哈希表来分组：

*   **哈希表结构**: `Map<String, List<String>>` (Java) 或 `dict[str, list[str]]` (Python)。
    *   **键 (Key)**: 字符串的规范化表示（例如，通过字符计数生成的字符串）。
    *   **值 (Value)**: 一个列表，存储所有映射到这个键的原始字符串（即它们是字母异位词）。

**算法流程：**

1.  创建一个空的哈希表 `anagramGroups`。
2.  遍历输入的字符串数组 `strs` 中的每一个字符串 `s`。
3.  对于每个字符串 `s`：
    a.  **生成键**: 计算 `s` 中每个字符的频率，并将其转换为一个唯一的字符串键 `key`。
    b.  **分组**:
        *   检查 `anagramGroups` 中是否已经存在 `key`。
        *   如果 `key` **不存在**：说明这是第一次遇到这种字符组合的字符串。创建一个新的空列表 `listForGroup`，将 `s` 加入到 `listForGroup` 中，然后将 `(key, listForGroup)` 存入 `anagramGroups`。
        *   如果 `key` **已经存在**：说明之前已经遇到过这种字符组合的字符串。从 `anagramGroups` 中取出与 `key` 关联的现有列表 `listForGroup`，将 `s` 加入到 `listForGroup` 中。
4.  遍历完所有字符串后，哈希表的 `values()`（所有列表）就是我们所需的分组结果。将其转换为 `List<List<String>>` 并返回。

---

 4. 算法步骤详解 (字符计数法)

1.  **初始化**:
    *   创建一个空的 `HashMap<String, List<String>> anagramGroups = new HashMap<>();` (Java) 或 `anagram_groups = {}` (Python)。

2.  **遍历输入数组**:
    *   对于 `strs` 数组中的每个字符串 `s`：

        a.  **创建频率数组**:
            *   定义一个 `int[] charCounts = new int[26];` (Java) 或 `char_counts = [0] * 26` (Python)。这将存储 'a' 到 'z' 的出现次数。

        b.  **填充频率数组**:
            *   遍历当前字符串 `s` 中的每个字符 `c`：
                *   将 `charCounts[c - 'a']` 对应位置的计数加 1。

        c.  **生成唯一键**:
            *   在 Java 中，最简单的方法是 `String key = Arrays.toString(charCounts);`。这会生成一个类似 `"[1, 0, 0, ..., 1, 0, 0, ..., 1]"` 的字符串。
            *   在 Python 中，将 `char_counts` 列表转换为元组 `key = tuple(char_counts)`。元组是不可变的，因此可以作为字典的键。

        d.  **存入哈希表**:
            *   使用 `HashMap.getOrDefault(key, new ArrayList<>())` (Java) 或 `dict.get(key, [])` (Python) 来获取与 `key` 关联的列表。如果 `key` 不存在，则返回一个新的空列表。
            *   将当前字符串 `s` 添加到这个列表中。
            *   使用 `HashMap.put(key, list)` (Java) 或 `dict[key] = list` (Python) 将更新后的列表重新存回哈希表。

3.  **收集结果**:
    *   所有字符串遍历完成后，哈希表 `anagramGroups` 的所有值 (`.values()`) 就是最终的分组结果。
    *   将这些值收集到一个 `List<List<String>>` (Java) 或 `list[list[str]]` (Python) 中并返回。

---

 5. 流程图


---

 6. Java 代码实现

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    /**
     * 将字母异位词组合在一起。
     * 使用字符计数法作为哈希表的键。
     *
     * @param strs 字符串数组。
     * @return 字母异位词分组后的列表。
     */
    public List<List<String>> groupAnagrams(String[] strs) {
        // 1. 初始化一个 HashMap，用于存储字母异位词的分组。
        // 键 (String): 字符串的规范化表示（这里是字符频率数组的字符串形式）。
        // 值 (List<String>): 存储所有属于该组的原始字符串。
        Map<String, List<String>> anagramGroups = new HashMap<>();

        // 2. 遍历输入的字符串数组
        for (String s : strs) {
            // a. 创建一个字符频率数组。
            // 数组大小为 26，因为只包含小写英文字母 'a' 到 'z'。
            // charCounts[0] 对应 'a' 的频率，charCounts[1] 对应 'b'，以此类推。
            int[] charCounts = new int[26];

            // b. 填充频率数组：统计当前字符串 s 中每个字符的出现次数。
            for (char c : s.toCharArray()) {
                charCounts[c - 'a']++; // 'a' 的 ASCII 码减 'a' 为 0，'b' 为 1，以此类推。
            }

            // c. 生成唯一键：将频率数组转换为一个字符串作为 HashMap 的键。
            // Arrays.toString(charCounts) 会生成一个形如 "[x, y, z, ...]" 的字符串，
            // 它是唯一的，可以作为字母异位词组的标识符。
            String key = Arrays.toString(charCounts);

            // d. 存入哈希表：将当前字符串 s 加入到对应的分组中。
            // HashMap.getOrDefault(key, defaultValue) 方法会尝试获取 key 对应的值。
            // 如果 key 存在，则返回其对应的值；如果不存在，则返回 defaultValue（这里是一个新的 ArrayList）。
            List<String> listForGroup = anagramGroups.getOrDefault(key, new ArrayList<>());
            listForGroup.add(s); // 将当前字符串 s 添加到列表中

            // 将更新后的列表重新存回 HashMap。
            // 如果 key 是新创建的，则会添加新的键值对；如果 key 已经存在，则会更新其值。
            anagramGroups.put(key, listForGroup);
        }

        // 3. 收集结果：将 HashMap 中所有的值（即所有分组的列表）收集到一个新的列表中并返回。
        return new ArrayList<>(anagramGroups.values());
    }
}
```

---

 7. Python 代码实现

```python
from collections import defaultdict

class Solution:
    """
    将字母异位词组合在一起。
    使用字符计数法作为字典的键。
    """
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        # 1. 初始化一个 defaultdict。
        # defaultdict 是一种特殊的字典，当访问一个不存在的键时，它会自动调用工厂函数（这里是 list）
        # 来为该键创建一个默认值（这里是一个空列表），而不会抛出 KeyError。
        # 键 (tuple): 字符串的规范化表示（这里是字符频率列表转换成的元组）。
        # 值 (list[str]): 存储所有属于该组的原始字符串。
        anagram_groups = defaultdict(list)

        # 2. 遍历输入的字符串列表
        for s in strs:
            # a. 创建一个字符频率列表。
            # 列表大小为 26，因为只包含小写英文字母 'a' 到 'z'。
            # char_counts[0] 对应 'a' 的频率，char_counts[1] 对应 'b'，以此类推。
            char_counts = [0] * 26

            # b. 填充频率列表：统计当前字符串 s 中每个字符的出现次数。
            for char_code in map(ord, s): # 使用 map(ord, s) 将字符转换为其 ASCII 值
                char_counts[char_code - ord('a')] += 1 # ord('a') 获取 'a' 的 ASCII 值

            # c. 生成唯一键：将频率列表转换为一个元组作为字典的键。
            # 列表是可变的，不能直接作为字典的键。元组是不可变的，因此可以作为键。
            key = tuple(char_counts)

            # d. 存入字典：将当前字符串 s 加入到对应的分组中。
            # 由于使用了 defaultdict，如果 key 不存在，它会自动创建一个空列表，然后我们直接向其添加 s。
            anagram_groups[key].append(s)

        # 3. 收集结果：将字典中所有的值（即所有分组的列表）收集到一个新的列表中并返回。
        return list(anagram_groups.values())

```

---

 8. 示例演练

我们以 `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]` 为例，逐步演示 Java 代码的执行过程：

*   `anagramGroups` 初始化为 `{}`。

1.  **处理 "eat"**:
    *   `charCounts` for "eat": `[1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0]` (a:1, e:1, t:1, others:0)
    *   `key = "[1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]"`
    *   `anagramGroups.getOrDefault(key, new ArrayList<>())` -> 返回 `new ArrayList<>()` (因为 key 不存在)
    *   `listForGroup.add("eat")` -> `["eat"]`
    *   `anagramGroups.put(key, ["eat"])` -> `anagramGroups = { key: ["eat"] }`

2.  **处理 "tea"**:
    *   `charCounts` for "tea": `[1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0]` (同上)
    *   `key` (同上)
    *   `anagramGroups.getOrDefault(key, new ArrayList<>())` -> 返回 `["eat"]` (因为 key 已存在)
    *   `listForGroup.add("tea")` -> `["eat", "tea"]`
    *   `anagramGroups.put(key, ["eat", "tea"])` -> `anagramGroups = { key: ["eat", "tea"] }`

3.  **处理 "tan"**:
    *   `charCounts` for "tan": `[1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0]` (a:1, n:1, t:1)
    *   `key2 = "[1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]"`
    *   `anagramGroups.getOrDefault(key2, new ArrayList<>())` -> 返回 `new ArrayList<>()`
    *   `listForGroup.add("tan")` -> `["tan"]`
    *   `anagramGroups.put(key2, ["tan"])` -> `anagramGroups = { key: ["eat", "tea"], key2: ["tan"] }`

4.  **处理 "ate"**:
    *   `charCounts` for "ate": `[1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0]` (同 `key`)
    *   `key` (同 `key`)
    *   `anagramGroups.getOrDefault(key, new ArrayList<>())` -> 返回 `["eat", "tea"]`
    *   `listForGroup.add("ate")` -> `["eat", "tea", "ate"]`
    *   `anagramGroups.put(key, ["eat", "tea", "ate"])` -> `anagramGroups = { key: ["eat", "tea", "ate"], key2: ["tan"] }`

5.  **处理 "nat"**:
    *   `charCounts` for "nat": `[1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0]` (同 `key2`)
    *   `key2` (同 `key2`)
    *   `anagramGroups.getOrDefault(key2, new ArrayList<>())` -> 返回 `["tan"]`
    *   `listForGroup.add("nat")` -> `["tan", "nat"]`
    *   `anagramGroups.put(key2, ["tan", "nat"])` -> `anagramGroups = { key: ["eat", "tea", "ate"], key2: ["tan", "nat"] }`

6.  **处理 "bat"**:
    *   `charCounts` for "bat": `[1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0]` (a:1, b:1, t:1)
    *   `key3 = "[1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]"`
    *   `anagramGroups.getOrDefault(key3, new ArrayList<>())` -> 返回 `new ArrayList<>()`
    *   `listForGroup.add("bat")` -> `["bat"]`
    *   `anagramGroups.put(key3, ["bat"])` -> `anagramGroups = { key: ["eat", "tea", "ate"], key2: ["tan", "nat"], key3: ["bat"] }`

最后，返回 `new ArrayList<>(anagramGroups.values())`，结果可能类似 `[["bat"], ["tan", "nat"], ["eat", "tea", "ate"]]`。

---

 9. 复杂度分析

*   **时间复杂度**: `O(N * L)`。
    *   `N` 是输入字符串数组 `strs` 的长度。
    *   `L` 是字符串 `strs[i]` 的最大长度。
    *   外层循环遍历 `N` 个字符串。
    *   在每次迭代中：
        *   填充 `charCounts` 数组需要遍历当前字符串，时间复杂度为 `O(L)`。
        *   将 `charCounts` 转换为 `key` (字符串) 在 Java 中 `Arrays.toString()` 是 `O(26)` (常数时间)。在 Python 中 `tuple()` 也是 `O(26)`。
        *   HashMap/Dictionary 的 `put`/`get` 操作平均时间复杂度是 `O(1)`。
    *   因此，总的时间复杂度是 `N * (O(L) + O(26) + O(1)) = O(N * L)`。
    *   对于 `N = 10^4`, `L = 100`，总操作次数约为 `10^4 * 100 = 10^6`，这在 1 秒内是完全可以接受的。

*   **空间复杂度**: `O(N * L)`。
    *   在最坏情况下，所有字符串都不是字母异位词，那么 HashMap 中会有 `N` 个不同的键。
    *   每个键对应的值是一个 `List<String>`，其中存储了原始字符串。所有原始字符串的总长度是 `N * L`。
    *   `charCounts` 数组占用 `O(26)` (常数) 空间。
    *   因此，主要的存储空间消耗在于 HashMap 中存储的所有字符串。最坏情况下是 `O(N * L)`。

---

希望这个极尽详细的讲解和代码能帮助你完全理解并掌握这道算法题！





### 128. 最长连续序列
已解答
中等
相关标签
premium lock icon
相关企业
给定一个未排序的整数数组 nums ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 O(n) 的算法解决此问题。

 

示例 1：

输入：nums = [100,4,200,1,3,2]
输出：4
解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。

示例 2：

输入：nums = [0,3,7,2,5,8,4,6,0,1]
输出：9

示例 3：

输入：nums = [1,0,1,2]
输出：3
 

提示：

0 <= nums.length <= 10^5
-10^9 <= nums[i] <= 10^9







#### 代码

```java
class Solution {
    public int longestConsecutive(int[] nums) {


        if( nums == null || nums.length == 0 ) {

            return 0;
        }

        Set<Integer> numSet = new HashSet<>();

        for ( int num : nums ) {

            numSet.add(num);
        }


        int longestConsecutive = 0;

        for( int num : numSet ) {
            // 这一步是关键修正：我们遍历的是去重后的 numSet，而不是原始的 nums 数组。
            // 这保证了每个唯一的数字作为潜在的序列起点只被检查一次。

            if( !numSet.contains( num - 1 ) ) {

                int currentNum = num;

                int currentStreak = 1;

                while( numSet.contains( currentNum + 1 ) ) {

                    currentNum++;

                    currentStreak++;
                }


                longestConsecutive = Math.max( longestConsecutive, currentStreak );
            

            }


    
        }
        
        return longestConsecutive;



    }
}
```


```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:


        if not nums:
            return 0

        num_set = set(nums)


        longest_streak = 0

        for num in num_set:
            if( num - 1 ) not in num_set:
                current_num = num
                current_streak = 1


                while( current_num + 1 ) in num_set:
                    current_num += 1
                    current_streak += 1

                longest_streak = max( longest_streak, current_streak )

        return longest_streak
        
```



#### 讲解




好的，作为一名高级软件工程师，我将极尽详细地为你讲解这道算法题，并分别提供 Java 和 Python 的代码实现。


 **1. 理解问题**

首先，我们来仔细理解一下题目要求：

*   **输入**: 一个未排序的整数数组 `nums`。
*   **目标**: 找出数字连续的最长序列的长度。
*   **特性**: 序列元素在原数组中**不要求连续**。例如，`[1, 3, 2]` 中 `[1, 2, 3]` 是连续序列。
*   **时间复杂度要求**: 必须设计并实现时间复杂度为 `O(n)` 的算法。
*   **约束**:
    *   `nums` 数组的长度在 0 到 10^5 之间。
    *   数组元素的值在 -10^9 到 10^9 之间。

**关键点**:

*   **未排序数组**: 不能直接利用排序特性进行线性扫描。
*   **连续序列**: 指的是数字上的连续，例如 `5, 6, 7`。
*   **不要求原数组连续**: 这是与“子数组”概念的区别，例如 `[1, 4, 2, 3]` 中 `[1, 2, 3, 4]` 是连续序列。
*   **`O(n)` 时间复杂度**: 这是最严格的约束，排除了基于排序的 `O(N log N)` 解决方案。这意味着我们需要一个接近单次遍历的算法，通常涉及哈希表。

**示例分析：**

*   `nums = [100,4,200,1,3,2]`
    *   连续序列有：
        *   `[100]`
        *   `[4]`
        *   `[200]`
        *   `[1, 2, 3, 4]` (由 1, 3, 2, 4 组成)
    *   最长的是 `[1, 2, 3, 4]`，长度为 4。

*   `nums = [0,3,7,2,5,8,4,6,0,1]`
    *   所有数字是 0, 1, 2, 3, 4, 5, 6, 7, 8。
    *   最长连续序列是 `[0, 1, 2, 3, 4, 5, 6, 7, 8]`，长度为 9。

---

 **2. 核心思想：哈希集合 (HashSet) + 优化查找**

为了实现 `O(n)` 的时间复杂度，我们首先想到使用哈希集合（`HashSet` 或 Python `set`），因为哈希集合提供了平均 `O(1)` 的查找、插入和删除操作。

**基本思路**:

1.  将所有数组元素放入一个哈希集合中。这样我们就可以快速地检查一个数字是否存在于数组中。
2.  遍历原始数组（或哈希集合中的每个数字）。对于每个数字 `num`，尝试以它为起点构建一个连续序列。
3.  在构建序列时，不断检查 `num + 1`, `num + 2`, ... 是否存在于哈希集合中，并计算当前序列的长度。

**关键优化 (避免重复计算)**:

如果只是简单地对每个数字都尝试构建序列，可能会导致重复计算。例如，对于序列 `[1, 2, 3, 4]`：
*   从 `1` 开始构建，会得到 `[1, 2, 3, 4]`，长度 4。
*   从 `2` 开始构建，会得到 `[2, 3, 4]`，长度 3。
*   从 `3` 开始构建，会得到 `[3, 4]`，长度 2。
*   从 `4` 开始构建，会得到 `[4]`，长度 1。

这样，`2, 3, 4` 都被多次检查了。为了避免这种冗余，我们只在 `num` 是一个连续序列的**起点**时才去构建它。

**如何判断一个数字 `num` 是否是某个连续序列的起点？**
如果 `num - 1` **不在**哈希集合中，那么 `num` 就是一个连续序列的起点。如果 `num - 1` 存在，说明 `num` 已经被包含在以 `num - 1` 为起点的某个序列中了，我们就不需要再从 `num` 开始重复构建了。

**优化后的算法流程**:

1.  将 `nums` 中的所有元素添加到 `HashSet` 中。
2.  初始化 `longestStreak = 0`。
3.  遍历 `nums` 中的每个数字 `num`。
4.  对于每个 `num`：
    *   **检查 `num - 1` 是否存在于 `HashSet` 中**:
        *   如果 `num - 1` **不存在**：说明 `num` 是一个潜在的连续序列的起点。
            *   初始化 `currentNum = num`。
            *   初始化 `currentStreak = 1`。
            *   **向右扩展序列**: `while (hashSet.contains(currentNum + 1))`：
                *   `currentNum` 增加 1。
                *   `currentStreak` 增加 1。
            *   更新 `longestStreak = Math.max(longestStreak, currentStreak)`。
        *   如果 `num - 1` **存在**：说明 `num` 不是一个新序列的起点，它已经是某个更早序列的一部分。跳过，不处理。
5.  返回 `longestStreak`。

---

 **3. 复杂度分析**

*   **时间复杂度**: `O(N)` (平均情况)
    *   将所有 `N` 个元素插入到 `HashSet` 中需要 `O(N)` 的平均时间。
    *   外层循环遍历 `N` 个元素。
    *   在内层 `while` 循环（向右扩展序列）中，每个数字 `x` 只会被 `hashSet.contains(x)` 检查一次。因为一旦 `x` 被包含在一个序列中，它就不会再作为起点被处理（因为 `x-1` 存在）。
    *   因此，虽然看起来有嵌套循环，但实际上每个数字在 `HashSet` 中的查找操作（`contains`）总共执行的次数是线性的，每个数字最多被访问常数次。
    *   所以，总的时间复杂度是 `O(N)`。

*   **空间复杂度**: `O(N)`
    *   为了存储所有 `N` 个元素到 `HashSet` 中，需要 `O(N)` 的额外空间。

---

 **4. 流程图**



---

 **5. Java 代码实现**（测试用例没有全部通过！后续有修正方法）

```java
import java.util.HashSet;
import java.util.Set;
import java.util.Arrays; // 导入 Arrays 只是为了调试或某些辅助操作，实际代码中未使用

class Solution {
    /**
     * 找出未排序整数数组中数字连续的最长序列的长度。
     * 使用哈希集合和优化查找的方法，时间复杂度为 O(n)。
     *
     * @param nums 输入的整数数组。
     * @return 最长连续序列的长度。
     */
    public int longestConsecutive(int[] nums) {
        // 1. 处理空数组的特殊情况
        if (nums == null || nums.length == 0) {
            return 0;
        }

        // 2. 将所有数组元素添加到哈希集合中，以便进行 O(1) 平均时间复杂度的查找。
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }

        // 3. 初始化最长连续序列的长度
        int longestStreak = 0;

        // 4. 遍历原始数组中的每个数字，尝试以它为起点构建连续序列。
        // 这里的关键优化是：只在 num 是一个序列的“起点”时才进行扩展。
        for (int num : nums) {
            // 检查 num - 1 是否存在于哈希集合中。
            // 如果 num - 1 不存在，则说明 num 是一个潜在的连续序列的起点。
            // 例如，对于 [1, 2, 3, 4]，当 num = 1 时，1-1=0 不存在，我们从 1 开始构建。
            // 当 num = 2 时，2-1=1 存在，说明 2 已经被包含在以 1 为起点的序列中，无需重复处理。
            if (!numSet.contains(num - 1)) {
                // 如果 num 是起点，初始化当前序列的数字和长度
                int currentNum = num;
                int currentStreak = 1;

                // 向右扩展序列：不断检查 currentNum + 1 是否存在。
                while (numSet.contains(currentNum + 1)) {
                    currentNum++;    // 移动到下一个连续数字
                    currentStreak++; // 增加当前序列的长度
                }

                // 更新全局最长连续序列的长度
                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }

        // 5. 返回最长连续序列的长度
        return longestStreak;
    }
}
```

---

 **6. Python 代码实现**（测试用例没有全部通过！后续有修正方法）

```python
class Solution:
    """
    找出未排序整数数组中数字连续的最长序列的长度。
    使用哈希集合和优化查找的方法，时间复杂度为 O(n)。
    """
    def longestConsecutive(self, nums: list[int]) -> int:
        # 1. 处理空数组的特殊情况
        if not nums:
            return 0

        # 2. 将所有数组元素添加到哈希集合中，以便进行 O(1) 平均时间复杂度的查找。
        num_set = set(nums)

        # 3. 初始化最长连续序列的长度
        longest_streak = 0

        # 4. 遍历原始数组中的每个数字，尝试以它为起点构建连续序列。
        # 这里的关键优化是：只在 num 是一个序列的“起点”时才进行扩展。
        for num in nums:
            # 检查 num - 1 是否存在于哈希集合中。
            # 如果 num - 1 不存在，则说明 num 是一个潜在的连续序列的起点。
            if (num - 1) not in num_set:
                # 如果 num 是起点，初始化当前序列的数字和长度
                current_num = num
                current_streak = 1

                # 向右扩展序列：不断检查 current_num + 1 是否存在。
                while (current_num + 1) in num_set:
                    current_num += 1    # 移动到下一个连续数字
                    current_streak += 1 # 增加当前序列的长度

                # 更新全局最长连续序列的长度
                longest_streak = max(longest_streak, current_streak)
        
        # 5. 返回最长连续序列的长度
        return longest_streak

```

---

 **7. 示例演练**

我们以 `nums = [100,4,200,1,3,2]` 为例，逐步演示 Java/Python 代码的执行过程：

*   **输入**: `nums = [100,4,200,1,3,2]`
*   **`numSet` (HashSet/set)**: `{100, 4, 200, 1, 3, 2}`
*   `longestStreak = 0`

**遍历 `nums`:**

1.  **`num = 100`**:
    *   `numSet.contains(99)`? -> `false`。(`100` 是起点)
    *   `currentNum = 100`, `currentStreak = 1`
    *   `while numSet.contains(101)`? -> `false`。
    *   `longestStreak = max(0, 1) = 1`.

2.  **`num = 4`**:
    *   `numSet.contains(3)`? -> `true`。(`4` 不是起点，跳过)

3.  **`num = 200`**:
    *   `numSet.contains(199)`? -> `false`。(`200` 是起点)
    *   `currentNum = 200`, `currentStreak = 1`
    *   `while numSet.contains(201)`? -> `false`。
    *   `longestStreak = max(1, 1) = 1`.

4.  **`num = 1`**:
    *   `numSet.contains(0)`? -> `false`。(`1` 是起点)
    *   `currentNum = 1`, `currentStreak = 1`
    *   `while numSet.contains(2)`? -> `true`。
        *   `currentNum = 2`, `currentStreak = 2`
    *   `while numSet.contains(3)`? -> `true`。
        *   `currentNum = 3`, `currentStreak = 3`
    *   `while numSet.contains(4)`? -> `true`。
        *   `currentNum = 4`, `currentStreak = 4`
    *   `while numSet.contains(5)`? -> `false`。
    *   `longestStreak = max(1, 4) = 4`.

5.  **`num = 3`**:
    *   `numSet.contains(2)`? -> `true`。(`3` 不是起点，跳过)

6.  **`num = 2`**:
    *   `numSet.contains(1)`? -> `true`。(`2` 不是起点，跳过)

遍历结束。

**返回 `longestStreak`，即 `4`。** 这与示例输出 `4` 完全一致。



希望这些极尽详细的讲解和代码能帮助你完全理解并掌握这两道算法题！


---



**修正：**
按照java解法，发现下面的测试用例超出时间限制

nums =略


你发现的这个问题非常敏锐且重要！在 LeetCode 的 128 题“最长连续序列”中，尽管我之前给出的算法思路和时间复杂度分析是正确的 (`O(N)`)，但实际的 Java 代码在面对包含大量重复数字的特定测试用例时，确实可能因为**对原始数组的重复遍历**而导致时间超限（Time Limit Exceeded, TLE）。

这通常发生在：
1.  输入数组 `nums` 包含大量重复数字。
2.  这些重复数字恰好是某个很长连续序列的“起点”。

例如你提供的测试用例：
`nums = [1,2,...,25000, 0,0,...,0]`
这里有 25000 个 `0`。在我的 Java 代码的 `for (int num : nums)` 循环中，每次遇到 `0`，`!numSet.contains(num - 1)` (即 `!numSet.contains(-1)`) 都会为 `true`，然后内层的 `while (numSet.contains(currentNum + 1))` 就会从 `0` 开始，一直向右查找并计算到 `25000`。这个过程会被重复执行 25000 次，导致 `25000 * 25000` 的操作量，即 `O(N * L)`（其中 L 是最长序列的长度），这显然超出了 `O(N)` 的要求。

**问题根源：**
`for (int num : nums)` 遍历的是原始数组，如果原始数组中有重复元素，且这些重复元素恰好是连续序列的“起点”，那么它们会重复触发内层 `while` 循环，导致总操作数增加。

**解决方案：**
非常简单，我们应该遍历**去重后的数字集合**，而不是原始数组。`HashSet` 在插入时会自动去重，所以我们只需要遍历 `HashSet` 中的元素即可。这样就能确保每个唯一的数字只被检查一次，从而严格保持 `O(N)` 的时间复杂度。

---

 **1. 修正后的核心思想回顾**

*   **哈希集合 (HashSet)**：将所有数字存入哈希集合，以便 `O(1)` 平均时间复杂度地检查数字是否存在。
*   **只从“真起点”开始扩展**: 对于哈希集合中的每个数字 `num`，如果 `num - 1` 不在集合中，那么 `num` 就是一个连续序列的起点。我们只从这些起点开始向右扩展序列并计算长度。这样可以避免重复计算已经被其他序列包含的数字。
*   **遍历去重后的集合**: 确保每个唯一的数字作为“起点”的检查只发生一次。

---

 **2. 修正后的 Java 代码实现**

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    /**
     * 找出未排序整数数组中数字连续的最长序列的长度。
     * 使用哈希集合和优化查找的方法，时间复杂度为 O(n)。
     *
     * @param nums 输入的整数数组。
     * @return 最长连续序列的长度。
     */
    public int longestConsecutive(int[] nums) {
        // 1. 处理空数组的特殊情况
        if (nums == null || nums.length == 0) {
            return 0;
        }

        // 2. 将所有数组元素添加到哈希集合中。
        // HashSet 会自动处理重复元素，确保 numSet 中只包含唯一的数字。
        // 这一步的时间复杂度是 O(N)，N 是 nums 的长度。
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }

        // 3. 初始化最长连续序列的长度
        int longestStreak = 0;

        // 4. 遍历哈希集合中的每个唯一的数字。
        // 这一步是关键修正：我们遍历的是去重后的 numSet，而不是原始的 nums 数组。
        // 这保证了每个唯一的数字作为潜在的序列起点只被检查一次。
        // 遍历 numSet 的时间复杂度是 O(M)，其中 M 是 numSet 的大小 (M <= N)。
        for (int num : numSet) { // <-- 关键修正：从 numSet 遍历
            // 检查 num - 1 是否存在于哈希集合中。
            // 如果 num - 1 不存在，则说明 num 是一个连续序列的“真起点”。
            // 只有真起点才需要我们去探索其后的连续数字，避免重复计算。
            // numSet.contains() 的平均时间复杂度是 O(1)。
            if (!numSet.contains(num - 1)) {
                // 如果 num 是真起点，初始化当前序列的数字和长度
                int currentNum = num;
                int currentStreak = 1;

                // 向右扩展序列：不断检查 currentNum + 1 是否存在于集合中。
                // 这一内部 while 循环的总执行次数是线性的。
                // 因为每个数字在 numSet 中只会被 'currentNum + 1' 访问一次。
                while (numSet.contains(currentNum + 1)) {
                    currentNum++;    // 移动到下一个连续数字
                    currentStreak++; // 增加当前序列的长度
                }

                // 更新全局最长连续序列的长度
                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }

        // 5. 返回最长连续序列的长度
        return longestStreak;
    }
}
```

---

 **3. 修正后的 Python 代码**

Python 的 `set(nums)` 会直接创建一个包含所有唯一元素的集合，后续的 `for num in num_set:` 循环自然就只遍历唯一的数字。

```python
class Solution:
    """
    找出未排序整数数组中数字连续的最长序列的长度。
    使用哈希集合和优化查找的方法，时间复杂度为 O(n)。
    """
    def longestConsecutive(self, nums: list[int]) -> int:
        # 1. 处理空数组的特殊情况
        if not nums:
            return 0

        # 2. 将所有数组元素添加到哈希集合中。
        # set(nums) 会自动创建包含唯一元素的集合。
        # 这一步的时间复杂度是 O(N)。
        num_set = set(nums)

        # 3. 初始化最长连续序列的长度
        longest_streak = 0

        # 4. 遍历哈希集合中的每个唯一数字。
        # 这一循环遍历的是去重后的集合，确保每个可能的序列起点只被检查一次。
        # 遍历 num_set 的时间复杂度是 O(M)，其中 M 是 num_set 的大小 (M <= N)。
        for num in num_set:
            # 检查 num - 1 是否存在于哈希集合中。
            # 如果 num - 1 不存在，则说明 num 是一个连续序列的“真起点”。
            # 'in' 运算符的平均时间复杂度是 O(1)。
            if (num - 1) not in num_set:
                # 如果 num 是真起点，初始化当前序列的数字和长度
                current_num = num
                current_streak = 1

                # 向右扩展序列：不断检查 current_num + 1 是否存在。
                # 这一内部 while 循环的总执行次数是线性的，因为每个数字只会被检查一次。
                while (current_num + 1) in num_set:
                    current_num += 1    # 移动到下一个连续数字
                    current_streak += 1 # 增加当前序列的长度

                # 更新全局最长连续序列的长度
                longest_streak = max(longest_streak, current_streak)
        
        # 5. 返回最长连续序列的长度
        return longest_streak

```

---

 **4. 最终复杂度分析**

经过修正后，Java 和 Python 解决方案的复杂度分析保持一致：

*   **时间复杂度**: `O(N)` (平均情况)
    *   将所有 `N` 个元素插入到 `HashSet`/`set` 中需要 `O(N)` 的平均时间。
    *   外层循环遍历 `HashSet`/`set` 中的 `M` 个唯一元素（`M <= N`）。
    *   内层 `while` 循环（向右扩展序列）中，每个数字 `x` 只会被 `contains(x)` 检查一次（因为一旦 `x` 被包含在一个序列中，它就不会再作为起点被处理）。
    *   因此，所有 `contains` 操作的总和不会超过 `O(N)`。
    *   所以，总的时间复杂度是 `O(N)`。

*   **空间复杂度**: `O(N)`
    *   为了存储所有 `N` 个（或 `M` 个唯一）元素到 `HashSet`/`set` 中，需要 `O(N)` 的额外空间。

这个修正后的 Java 代码应该能够顺利通过你遇到的超出时间限制的测试用例。




## 双指针













## 滑动窗口

















## 子串















## 普通数组







## 矩阵











## 链表











## 二叉树











## 图论











## 回溯











## 二分查找











## 栈











## 堆






## 贪心算法



## 动态规划




## 多维动态规划




## 技巧



