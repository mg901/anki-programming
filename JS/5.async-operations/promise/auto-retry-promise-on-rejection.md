## [Auto-retry Promise on rejection](https://bigfrontend.dev/problem/retry-promise-on-rejection)

```js
// Promises
function fetchWithAutoRetry(fetcher, maxRetries) {
  return fetcher().catch((reason) => {
    if (maxRetries === 0) {
      throw reason;
    }

    return fetchWithAutoRetry(fetcher, maxRetries - 1);
  });
}

// Async / await
async function fetchWithAutoRetry(fetcher, maxRetries) {
  try {
    return await fetcher();
  } catch (error) {
    if (maxRetries === 0) {
      throw error;
    }

    return fetchWithAutoRetry(fetcher, maxRetries - 1);
  }
}
```
