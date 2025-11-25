## [355 Design Twitter](https://leetcode.com/problems/design-twitter/description/)

[#lazy-refill]()

```js
class Twitter {
  #tweets = new Map();

  #followeeIds = new Map();

  #feedLimit = 10;

  #count = 0;

  postTweet(userId, tweetId) {
    if (!this.#tweets.has(userId)) {
      this.#tweets.set(userId, []);
    }

    const tweetsById = this.#tweets.get(userId);

    tweetsById.push({
      tweetId,
      count: this.#count,
    });

    this.#count += 1;

    if (tweetsById.length > this.#feedLimit) {
      tweetsById.shift();
    }
  }

  getNewsFeed(userId) {
    const followeeIds = this.#followeeIds.get(userId) ?? new Set();
    followeeIds.add(userId);

    const maxpq = new MaxPriorityQueue((tweet) => tweet.count);

    for (const followeeId of followeeIds) {
      if (!this.#tweets.has(followeeId)) continue;

      const tweetsById = this.#tweets.get(followeeId);
      const lastIndex = tweetsById.length - 1;

      maxpq.enqueue({
        ...tweetsById[lastIndex],
        followeeId,
        index: lastIndex - 1,
      });
    }

    const feed = [];

    while (!maxpq.isEmpty() && feed.length < this.#feedLimit) {
      const { tweetId, followeeId, index } = maxpq.dequeue();
      feed.push(tweetId);

      if (index >= 0) {
        maxpq.enqueue({
          ...this.#tweets.get(followeeId)[index],
          followeeId,
          index: index - 1,
        });
      }
    }

    return feed;
  }

  follow(followerId, followeeId) {
    if (!this.#followeeIds.has(followerId)) {
      this.#followeeIds.set(followerId, new Set());
    }

    this.#followeeIds.get(followerId).add(followeeId);
  }

  unfollow(followerId, followeeId) {
    this.#followeeIds.get(followerId)?.delete(followeeId);
  }
}
```
