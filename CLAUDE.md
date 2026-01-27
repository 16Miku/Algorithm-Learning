# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个算法学习笔记仓库，以 Markdown 文档形式记录 LeetCode、牛客网、企业笔试等平台的算法题目解答和学习笔记。

## 编程语言

- **主要语言**：Java（约440个代码块）
- **辅助语言**：Python（约155个代码块）
- 代码以代码块形式嵌入在 Markdown 文件中，无独立源代码文件

## 文档结构

| 文件 | 内容 |
|------|------|
| `数据结构与算法学习记录.md` | 综合学习记录（核心文档） |
| `LeetCode-Hot-100.md` | LeetCode 热题 100 |
| `滑动窗口与双指针.md` | 滑动窗口与双指针专题（灵神题单） |
| `笔试真题.md` | 企业笔试真题（蚂蚁、大疆、滴滴、小米、网易等） |
| `牛客ACM题库.md` | 牛客网 ACM 题库练习 |
| `二分算法.md` | 二分算法专题（灵神题单） |
| `字符串.md` | 字符串算法专题（灵神题单） |
| `ACM模式练习.md` | ACM 输入输出练习 |

## 题目记录格式

每道题目应遵循以下结构：

```markdown
### 题号. 题目名称

[题目描述、示例、提示]

#### 代码（无注释版）
```java
// 简洁实现
```

#### 代码（注释版）
```java
// 带详细注释的实现
```

#### 讲解
[算法思路、复杂度分析]
```

## 代码模式

### Core 模式（LeetCode 等平台）
```java
class Solution {
    public int method(int[] nums) {
        // 实现
    }
}
```

### ACM 模式（牛客、笔试等）
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        // 输入处理 + 实现 + 输出
    }
}
```

## 笔试真题命名规范

格式：`日期-公司-题号-题目名称-算法类型`

示例：
- 2025年8月10日-大疆-第一题-无人机能耗最小化路径规划-线性dp
- 2025年9月28日-网易-第一题-有序序列-基础语法

## 注意事项

- 添加新题目时，根据题目来源选择对应的 Markdown 文件
- 企业笔试题按日期和公司分类记录在 `笔试真题.md`
- 算法专题题目记录在对应的专题文件中
- 图片资源存放在 `image-ACM模式练习/` 目录

## 学习指导规则

### 用户背景

- 用户有 Java 基础，正在学习 Python
- 目标是突击准备笔试算法题
- 需要详细的 Python 语法讲解，并与 Java 对照

### 题目讲解格式

每道题目的讲解应包含：

1. **题目描述**：完整的题目、示例、提示
2. **代码（Java）**：带注释的 Java 解法
3. **代码（Python）**：带注释的 Python 解法
4. **讲解**：
   - 问题分析
   - 核心思想
   - 复杂度分析
5. **Python 基础知识补充**：
   - 本题涉及的 Python 语法详解
   - 代码逐行解析（带 Java 对照注释）
   - Java vs Python 对照表

### Python 语法讲解原则

- 每个新语法点都要与 Java 对照
- 提供可运行的代码示例
- 解释「为什么这样写」而不仅是「怎么写」
- 常见坑点要特别标注

### 代码注释风格

```python
# 创建默认值为空列表的字典
# 相当于 Java: Map<Key, List<String>> map = new HashMap<>();
anagram_groups = defaultdict(list)
```

### 训练计划

按照 `笔试算法突击训练方案.md` 中的 28 天计划进行：
- Day 1-7：高频基础题（哈希、双指针、滑动窗口、链表、栈）
- Day 8-14：核心算法（二分、二叉树、回溯）
- Day 15-21：动态规划专项
- Day 22-28：综合提升（图论、堆、贪心、技巧）

