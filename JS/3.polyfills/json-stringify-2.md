## [JSON.stringify 2](https://www.greatfrontend.com/questions/javascript/json-stringify-ii?language=js)

```js
function jsonStringify(data) {
  if (isCyclic(data)) {
    throw new TypeError('Converting circular structure to JSON');
  }

  const type = typeof data;

  if (type === 'bigint') {
    throw new TypeError('Do not know how to serialize a BigInt');
  }

  if (isNonSerializable(data)) {
    return undefined;
  }

  if (type === 'number') {
    if (Number.isNaN(data) || !Number.isFinite(data)) {
      return 'null';
    }

    return String(data);
  }

  if (data === null) {
    return 'null';
  }

  if (typeof data.toJSON === 'function') {
    return jsonStringify(data.toJSON());
  }

  if (Array.isArray(data)) {
    const result = data.map((x) => jsonStringify(x) ?? 'null').join(',');

    return `[${result}]`;
  }

  if (typeof data === 'object') {
    const result = [];

    for (const key in data) {
      if (Object.hasOwn(data, key)) {
        const value = data[key];

        if (value === undefined || isNonSerializable(value)) continue;

        result.push(`"${key}":${jsonStringify(value)}`);
      }
    }

    return `{${result.join(',')}}`;
  }

  if (type === 'string') {
    return `"${data.replace(/"/g, '\\"')}"`;
  }

  return String(data);
}

function isCyclic(value) {
  const visiting = new WeakSet();
  const visited = new WeakSet();

  return traverse(value);

  function traverse(data) {
    if (!data || typeof data !== 'object') return false;

    if (visiting.has(data)) return true;
    if (visited.has(data)) return false;

    visiting.add(data);

    for (const key in data) {
      if (Object.hasOwn(data, key) && traverse(data[key])) {
        return true;
      }
    }

    visiting.delete(data);
    visited.add(data);

    return false;
  }
}

function isNonSerializable(it) {
  const type = typeof it;

  return type === 'undefined' || type === 'function' || type === 'symbol';
}
```
