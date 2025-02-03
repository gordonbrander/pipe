# Pipe

Utils for piping and composing functions.

```typescript
import { flow, pipe } from "@gordonb/pipe";

const double = (n: number) => n * 2;
const addOne = (n: number) => n + 1;
const toString = (n: number) => n.toString();

const result = pipe(5, double, addOne, toString);
// "11"

const combined = flow(double, addOne, toString);
combined(5);
// "11"
```

This module offers four functions:

- `pipe(value, ...fns)` pipe value through one-argument functions, returning
  result.
- `pipeAsync(value, ...fns)` pipe value through async functions, returning
  promise for result. The return value of each step is awaited. The next
  function in the chain will receive the awaited value. pipeAsync allows using
  sync or async functions in the pipeline.
- `flow(...fns)` composes many one-argument functions into a single one-argument
  function that will apply them left-to-right. This is the opposite direction of
  traditional function composition, but it reads more nicely with the way
  JavaScript is typically read/written.
- `flowAsync(...fns)` composes many one-argument async functions into a single
  one-argument async function that will apply them left-to-right. flowAsync
  supports using both async and ordinary one-argument functions.

All functions support typesafe overloads for up to 20 functions.
