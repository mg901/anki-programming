## [API Retry 'promises'](https://frontendlead.com/coding-questions/api-retry)

<!-- notecardId: 1739474977117 -->

```js
function retryApiCall(fetcher, maxRetries, retryInterval) {
  let retries = maxRetries;

  return makeAttempt();

  function makeAttempt() {
    return fetcher()
      .then((response) => {
        if (response.status !== 200) {
          return retryOnFail();
        }

        return response;
      })
      .catch(retryOnFail);
  }

  function retryOnFail() {
    retries -= 1;

    if (retries === 0) {
      throw new Error(`API call failed after ${maxRetries} retries`);
    } else {
      return new Promise((resolve) => {
        setTimeout(resolve, retryInterval);
      }).then(makeAttempt);
    }
  }
}
```

## [API Retry 'async/await'](https://frontendlead.com/coding-questions/api-retry)

<!-- notecardId: 1739474977120 -->

```js
async function retryApiCall(fetcher, maxRetries, duration) {
  for (let i = 0; i < maxRetries; i += 1) {
    try {
      const response = await fetcher();

      if (response.status === 200) {
        return response;
      } else {
        retryOnFail(duration);
      }
    } catch (error) {
      retryOnFail(duration);
    }
  }

  throw new Error(`API call failed after ${maxRetries} retries`);
}

async function retryOnFail(duration) {
  await new Promise((resolve) => {
    setTimeout(resolve, duration);
  });
}
```
