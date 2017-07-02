---
layout: post
title: Add Two Numbers
tags: Leetcode题解
---
# 题目描述:
给两个用非空链表表示的正整数，按链表头节点存储个位，十位百位……依次排列的顺序将每个数据位存储在一个链表的节点中，将两个链表相加并返回其和的链表形式(表示方法同输入链表)。假设正整数除非本身是0,否则不会以0开头。
[原体目](https://leetcode.com/problems/add-two-numbers)

# 问题分析：
这是一个考察链表操作的题目。如果熟悉链表操作，这个问题将非常简单。
有几点需要注意：
- 并不能保证这两个链表是等长的，比如说输入了5, 555两个数。其中短数的部分可以用0填充。
- 低位相加后如果大于9需要进位，最高位进位后所得的和链表比两个输入链表都多一个值为一的节点。

# C++代码示例：
{% highlight C++ %}
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

#include <vector>
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto h1 = l1;
        auto h2 = l2;
        int flag = 0;
        ListNode* head;
        ListNode* hd = NULL;
        while (h1 != NULL || h2 != NULL) {
            int a = 0;
            int b = 0;
            if (h1 != NULL) {
                a = h1->val;
                h1 = h1->next;
            }

            if (h2 != NULL) {
                b = h2->val;
                h2 = h2->next;
            }
            if (hd == NULL) {
                hd = new ListNode((a+b+flag)%10);
                head = hd;
            } else {
                hd->next = new ListNode((a+b+flag)%10);
                hd = hd->next;
            }

            if ((a+b+flag)>9)
                flag = 1;
            else
                flag = 0;

        }
        if (flag == 1) {
            auto n = new ListNode(flag);
            hd->next = n;
        }
        return head;
    }
};
{% endhighlight %}
