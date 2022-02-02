---
layout: single
title: "[Tree] Binary Tree to Linked List."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
/**
 * class Tree {
 *     public:
 *         int val;
 *         Tree *left;
 *         Tree *right;
 * };
 */

/**
 * class LLNode {
 *     public:
 *         int val;
 *         LLNode *next;
 * };
 */
LLNode* head;
LLNode* dummy;
void help(Tree* root){
    if(!root) return;
    help(root->left);
    LLNode *newNode = new LLNode();
    newNode->val = root->val;
    dummy->next = newNode;
    dummy = dummy->next;
    help(root->right);
}
LLNode* solve(Tree* root) {
    head = new LLNode();
    dummy = head;
    help(root);
    return head->next;
}
```