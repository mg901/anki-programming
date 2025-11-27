## [355 Design Twitter](https://leetcode.com/problems/design-twitter/description/)

[#lazy-refill]()

```js
class Twitter {
  #tweets = new Map();

  #followeeIds = new Map();

  #feedLimit = 10;

  #count = 0;

  postTweet(userId, tweetId) {
    const tweets = this.#tweets.get(userId) ?? [];
    this.#tweets.set(userId, tweets);

    if (tweets.length > this.#feedLimit) {
      tweets.shift();
    }

    this.#count += 1;

    tweets.push({
      tweetId,
      count: this.#count,
    });
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
    let followeeIds = this.#followeeIds.get(followerId);

    if (!followeeIds) {
      followeeIds = new Set();
      this.#followeeIds.set(followerId, followeeIds);
    }

    followeeIds.add(followeeId);
  }

  unfollow(followerId, followeeId) {
    this.#followeeIds.get(followerId)?.delete(followeeId);
  }
}
```
