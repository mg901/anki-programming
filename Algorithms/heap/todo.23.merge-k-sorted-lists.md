## [23 Merge k Sorted Lists 'heap'](https://leetcode.com/problems/merge-k-sorted-lists/description/)

```js
function mergeKLists(lists) {
  const minpq = new MinPriorityQueue((node) => node.val);

  for (const node of lists) {
    if (!node) continue;

    minpq.enqueue(node);
  }

  let head = null;
  let tail = null;

  while (!minpq.isEmpty()) {
    const node = minpq.dequeue();

    if (!head) {
      head = node;
      tail = node;
    } else {
      tail.next = node;
      tail = node;
    }

    if (node.next) minpq.enqueue(node.next);
  }

  return head;
}
```
