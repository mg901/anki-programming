## [105 Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

<!-- notecardId: 1742467194947 -->

```js
function buildTree(preorder, inorder) {
  let preIdx = 0;
  let inIdx = 0;

  return traverse();

  function traverse(stop) {
    if (inorder[inIdx] === stop) return null;

    const node = new Node(preorder[preIdx]);
    preIdx += 1;

    node.left = traverse(node.val);
    inIdx += 1;
    node.right = traverse(stop);

    return node;
  }
}
```
