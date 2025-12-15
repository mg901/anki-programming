## [Binary Tree](https://www.greatfrontend.com/questions/algo/binary-tree)

<!-- notecardId: 1765809477650 -->

```js
export class BinaryTreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

export class BinaryTree {
  constructor(value) {
    this.root = value ? new BinaryTreeNode(value) : null;
  }

  size() {
    return this.root ? dfs(this.root) : 0;

    function dfs(node) {
      if (!node) return 0;

      return 1 + dfs(node.left) + dfs(node.right);
    }
  }

  height() {
    return !this.root ? 0 : dfs(this.root);

    function dfs(node) {
      if (!node) return -1;

      return 1 + Math.max(dfs(node.left), dfs(node.right));
    }
  }

  inOrder() {
    const root = this.root;
    if (!root) return [];

    const stack = [];
    let current = root;
    const result = [];

    while (current || stack.length) {
      while (current) {
        stack.push(current);
        current = current.left;
      }

      current = stack.pop();
      result.push(current.value);
      current = current.right;
    }

    return result;
  }

  preOrder() {
    const root = this.root;
    if (!root) return [];

    const stack = [root];
    const result = [];

    while (stack.length) {
      const node = stack.pop();
      result.push(node.value);

      if (node.right) stack.push(node.right);
      if (node.left) stack.push(node.left);
    }

    return result;
  }

  postOrder() {
    const root = this.root;
    if (!root) return [];

    const result = [];
    const stack = [root];

    while (stack.length) {
      const node = stack.pop();
      result.push(node.value);

      if (node.left) stack.push(node.left);
      if (node.right) stack.push(node.right);
    }

    return result.reverse();
  }

  isBalanced() {
    return dfs(this.root) !== -1;

    function dfs(node) {
      if (!node) return 0;

      const left = dfs(node.left);
      const right = dfs(node.right);

      if (left === -1 || right === -1 || Math.abs(left - right) > 1) {
        return -1;
      }

      return 1 + Math.max(left, right);
    }
  }

  isComplete() {
    const queue = [this.root];
    let seeNull = false;

    while (queue.length) {
      const node = queue.shift();

      if (node === null) {
        seeNull = true;
        continue;
      }

      if (seeNull) return false;

      queue.push(node.left);
      queue.push(node.right);
    }

    return true;
  }
}
```
