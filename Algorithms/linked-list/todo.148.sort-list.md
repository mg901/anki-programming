## [148 Sort List](https://leetcode.com/problems/sort-list/description/)

<!-- notecardId: 1764668743629 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/TGveA1oFhrc

// - Time: O(n log(n))
// - Space: O(n log(n))
function sortList(head) {
  if (!head || !head.next) return head;

  const [prev, mid] = findMid(head);
  prev.next = null;

  return mergeTwoLists(sortList(head), sortList(mid));
}

function findMid(head) {
  let slow = head;
  let fast = head;
  let prev = null;

  while (fast && fast.next) {
    prev = slow;
    slow = slow.next;
    fast = fast.next.next;
  }

  return [prev, slow];
}

function mergeTwoLists(list1, list2) {
  if (!list1) return list2;
  if (!list2) return list1;

  let head = null;

  if (list1.val <= list2.val) {
    head = list1;
    list1 = list1.next;
  } else {
    head = list2;
    list2 = list2.next;
  }

  let current = head;

  while (list1 && list2) {
    if (list1.val <= list2.val) {
      current.next = list1;
      list1 = list1.next;
    } else {
      current.next = list2;
      list2 = list2.next;
    }

    current = current.next;
  }

  current.next = list1 || list2;

  return head;
}
```

## [148 Sort List 'space-optimized'](https://leetcode.com/problems/sort-list/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/TGveA1oFhrc
// - Time: O(n log(n))
// - Space: O(1)
function sortList(head) {
  if (!head || !head.next) return head;

  let length = 0;
  let current = head;

  while (current) {
    current = current.next;
    length += 1;
  }

  const dummy = new ListNode(0, head);

  for (let step = 1; step < length; step *= 2) {
    let curr = dummy.next;
    let tail = dummy;

    while (curr) {
      const left = curr;
      const right = split(left, step);
      curr = split(right, step);
      tail = merge(left, right, tail);
    }
  }

  return dummy.next;
}

function split(head, n) {
  for (let i = 1; i < n && head; i += 1) {
    head = head.next;
  }

  if (!head) return null;
  const { next } = head;
  head.next = null;

  return next;
}

function merge(l1, l2, tail) {
  let current = tail;

  while (l1 && l2) {
    if (l1.val <= l2.val) {
      current.next = l1;
      current = l1;
      l1 = l1.next;
    } else {
      current.next = l2;
      current = l2;
      l2 = l2.next;
    }
  }

  current.next = l1 || l2;

  while (current.next) {
    current = current.next;
  }

  return current;
}
```
