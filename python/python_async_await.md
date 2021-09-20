# python async & await

Inspired by and examples from https://www.heise.de/hintergrund/async-await-in-Python-Nebenlaeufigkeit-leicht-gemacht-6193925.html

---

Only `async` functions can `await` other `async` functions.

```python
import asyncio

async def foo():
  await asyncio.sleep(1)

async def bar():
  x = await foo()
```

Note that `await foo()` is correct, but `await foo` is wrong.
Calling `foo()` returns a `Future`, which gets awaited with `await`.
You can't await a function.

You can use `async def` everywhere you can use a `def` — even in `class`.

```python
class MyClass():
  async def soSomething():
    await foo()
```

A coroutine has to run in an event loop.
`asyncio.run()` creates such an event loop and waits until it finishes.

```python
import asyncio

async def main():
  pass

if __name__ == "__main__":
  asyncio.run(main())
```

Avoid blocking io, like

```python
async def read():
  with open("myfile.txt") as file:
    return file.read()
```

You can start a coroutine with `asyncio.create_task()` and `await` the result later.
Thus, several corotines can run concurrent.

```python
# The following takes 2 seconds to execute.
await asyncio.sleep(1)
await asyncio.sleep(1)

# The following just takes 1 second to execute.
task1 = asyncio.create_task(asyncio.sleep(1))
task2 = asyncio.create_task(asyncio.sleep(1))
await task1
await task2
```

Start coroutines and specify when to return.
Then `done` contains the task that are finish and `pending` contains task that are not finished yet.

```python
done, pending = await asyncio.wait([asyncio.sleep(i) for i in range(3)], return_when="FIRST_COMPLETED")
done, pending = await asyncio.wait([asyncio.sleep(i) for i in range(3)], return_when="ALL_COMPLETED")
done, pending = await asyncio.wait([asyncio.sleep(i) for i in range(3)], return_when="FIRST_EXCEPTION")
```

Tasks can be awaited multiple times (Multiple `process()` functions await `database_request()`).
Furthermore you can handle tasks in the order in which they finish their execution with `asyncio.as_completed()`.

```python
async def database_request():
  await asyncio.sleep(1)
  return "Data"

async def process(data):
  print(await data)

async def main():
  data = asyncio.create_task(database_request())
  
  tasks = [asyncio.create_task(process(data)) for _ in range(3)]
  for completed_task in asyncio.as_completed(tasks):
    await completed_task
  ```
