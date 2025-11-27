## [23 Merge k Sorted Lists 'heap'](https://leetcode.com/problems/merge-k-sorted-lists/description/)

```js
function mergeKLists(lists) {
  const minpq = new MinPriorityQueue((node) => node.val);

  for (const node of lists) {
    if (node) {
      minpq.enqueue(node);
    }
  }

  const dummy = new ListNode(0);
  let current = dummy;

  while (!minpq.isEmpty()) {
    const node = minpq.dequeue();
    if (node.next) minpq.enqueue(node.next);

    current.next = node;
    current = current.next;
  }

  return dummy.next;
}
```
