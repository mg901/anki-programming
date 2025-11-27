## [621 Task Scheduler](https://leetcode.com/problems/task-scheduler/description/)

```js
function leastInterval(tasks, n) {
  const counter = new Map();

  for (const task of tasks) {
    counter.set(task, (counter.get(task) ?? 0) + 1);
  }

  const maxpq = new MaxPriorityQueue();

  for (const freq of counter.values()) {
    maxpq.enqueue(freq);
  }

  let time = 0;
  const queue = new Queue();

  while (maxpq.size() > 0 || queue.size() > 0) {
    time += 1;

    if (maxpq.size() > 0) {
      const remaining = maxpq.dequeue() - 1;

      if (remaining > 0) {
        queue.enqueue([remaining, time + n]);
      }
    }

    if (queue.size() > 0 && queue.front().at(1) === time) {
      maxpq.enqueue(queue.dequeue().at(0));
    }
  }

  return time;
}
```
