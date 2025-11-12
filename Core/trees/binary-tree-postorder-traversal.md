## [Binary Tree Postorder Traversal 'imperative'](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)

```js
// - Time: O(n)
// - Space: O(n)
function postorderTraversal(root) {
  if (!root) return [];

  let stack = [root];
  let result = [];

  while (stack.length) {
    const node = stack.pop();
    result.push(node.val);

    if (node.left) stack.push(node.left);
    if (node.right) stack.push(node.right);
  }

  return result.reverse();
}
```
