## [Call APIs with pagination 'promises'](https://bigfrontend.dev/problem/call-APIs-with-pagination)

```js
const fetchListWithAmount = async (amount = 5) => {
  const result = [];

  return makeFetch();

  function makeFetch(id) {
    return fetchList(id).then(({ items }) => {
      if (!items.length) return result;

      result.push(...items);

      if (result.length < amount) {
        const lastItemId = items.at(-1).id;

        return makeFetch(lastItemId);
      }

      return result.slice(0, amount);
    });
  }
};
```

## [Call APIs with pagination 'async/await'](https://bigfrontend.dev/problem/call-APIs-with-pagination)

```js
const fetchListWithAmount = async (amount = 5) => {
  let result = [];

  try {
    return await makeFetch();
  } catch (error) {
    throw error;
  }

  async function makeFetch(id) {
    const response = await fetchList(id);
    const { items } = response;

    if (!items.length) return result;

    result.push(...items);

    if (result.length < amount) {
      const lastItemId = items.at(-1).id;

      return await makeFetch(lastItemId);
    }

    return result.slice(0, amount);
  }
};

const fetchListWithAmount = async (amount = 5) => {
  const result = [];
  let lastItemId;

  try {
    while (true) {
      const { items } = await fetchList(lastItemId);
      if (!items.length) break;

      result.push(...items);
      if (result.length >= amount) break;

      lastItemId = items.at(-1).id;
    }
  } catch (error) {
    throw error;
  }

  return result.slice(0, amount);
};
```

## [Call APIs with pagination 'generator'](https://bigfrontend.dev/problem/call-APIs-with-pagination)

```js
const fetchListWithAmount = async (amount = 5) => {
  const result = [];
  const generator = fetchListWithAmountGenerator(amount);
  let next = generator.next();

  while (!next.done) {
    try {
      const response = await next.value;
      const { items } = response;

      if (!items.length) break;

      result.push(...items);

      next = generator.next(items);
    } catch (error) {
      try {
        generator.throw(error);
      } catch (error) {
        throw error;
      }
    }
  }

  return result.slice(0, amount);
};

function* fetchListWithAmountGenerator(amount = 5) {
  let lastItemId;
  let dataLength = 0;

  while (dataLength < amount) {
    const items = yield fetchList(lastItemId);

    dataLength += items.length;
    lastItemId = items.at(-1).id;
  }
}
```

## [Call APIs with pagination 'async generator'](https://bigfrontend.dev/problem/call-APIs-with-pagination)

```js
const fetchListWithAmount = async (amount = 5) => {
  const result = [];
  const asyncGenerator = fetchListWithAmountGenerator(amount);

  try {
    for await (const items of asyncGenerator) {
      result.push(...items);
    }
  } catch (error) {
    throw error;
  }

  return result.slice(0, amount);
};

async function* fetchListWithAmountGenerator(amount = 5) {
  let lastItemId;
  let dataLength = 0;

  while (dataLength < amount) {
    const response = await fetchList(lastItemId);
    const { items } = response;

    if (!items.length) break;

    yield items;

    dataLength += items.length;
    lastItemId = items.at(-1).id;
  }
}
```
