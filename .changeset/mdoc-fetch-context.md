---
"@owf/mdoc": minor
---

**Breaking:** `MdocContext.fetch` takes a third argument naming what is being retrieved, `{ type: 'statusList' | 'identifierList' }`, so an implementation can apply caching, timeouts or retries per resource instead of to every request alike. Those revocation lists are currently the only resources the library fetches.

Most implementations need no change: the global `fetch` satisfies the callback, as do implementations that name their parameters or declare fewer of them. One written with a rest parameter has to name its parameters, since a three-element tuple cannot be spread into the two-parameter global.

```diff
-fetch: (...args) => fetch(...args),
+fetch: (input, init) => fetch(input, init),
```

Nothing changes at runtime. An implementation that ignores the third argument behaves exactly as before.
