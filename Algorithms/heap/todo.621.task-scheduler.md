## [621 Task Scheduler](https://leetcode.com/problems/task-scheduler/description/)

```js
function leastInterval(tasks, n) {
  const charFreq = new Map();

  for (const task of tasks) {
    charFreq.set(task, (charFreq.get(task) ?? 0) + 1);
  }

  const maxHeap = new MaxPriorityQueue();

  for (const freq of charFreq.values()) {
    maxHeap.enqueue(freq);
  }

  let time = 0;
  const queue = new Queue();

  while (maxHeap.size() > 0 || queue.size() > 0) {
    time += 1;

    if (maxHeap.size() > 0) {
      const remaining = maxHeap.dequeue() - 1;

      if (remaining > 0) {
        queue.enqueue([remaining, time + n]);
      }
    }

    if (queue.size() > 0 && queue.front().at(1) === time) {
      maxHeap.enqueue(queue.dequeue().at(0));
    }
  }

  return time;
}
```
