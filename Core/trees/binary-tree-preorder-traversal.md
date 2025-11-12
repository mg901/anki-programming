## [Binary Tree Preorder Traversal 'imperative'](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

```js
// - Time: O(n)
// - Space: O(n)
function preorderTraversal(root) {
  if (!root) return [];

  const result = [];
  const stack = [root];

  while (stack.length) {
    let node = stack.pop();

    result.push(node.val);

    if (node.right) stack.push(node.right);
    if (node.left) stack.push(node.left);
  }

  return result;
}
```
