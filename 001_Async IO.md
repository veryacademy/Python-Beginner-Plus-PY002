# asyncio/async await

```python 
# Introduction Example
# synchronous
def task1():
    print('Send first Email')
    print('First Email reply')
    task2()

def task2():
    print('Send second Email')
    print('Second Email reply')
    task3()

def task3():
    print('Send third Email')
    print('Third Email reply')
    print("====")
    print("END")

task1()

# asynchronous

import asyncio

async def task1():
    print('Send first Email')
    asyncio.create_task(task2())
    await asyncio.sleep(2) # Simulating that the email reply takes 2 seconds
    print('First Email reply')

async def task2():
    print('Send second Email')
    asyncio.create_task(task3())
    await asyncio.sleep(2)
    print('Second Email reply')

async def task3():
    print('Send third Email')
    await asyncio.sleep(2)
    print('Third Email reply')

asyncio.run(task1())
```

```python
# 1.0.1 Coroutine objects
import asyncio

# Python 3.3
@asyncio.coroutine 
def load_file(path):
    pass

# Python 3.5
async def send_email():
    pass
```
```python
# 1.0.2 Determine if a function is a coroutine or not
import asyncio

async def task1():
    pass
   
print(asyncio.iscoroutinefunction(task1))

# asyncio.iscoroutinefunction(func)
# asyncio.iscoroutine(obj)
```
```python
# 1.0.3 Run with asyncio
import asyncio
async def task1():
    print("Ping")

# Creates event loop
asyncio.run(task1())
```
```python
# 1.0.4 Wait for a task
import asyncio
async def task1():
    print("1")
    await asyncio.sleep(1)
    print("2")

asyncio.run(task1())
```
```python
# 1.0.5 Chaining Coroutines
import asyncio

async def t1():
    await t2()
    print("t1")
async def t2():
    await t3()
    print("t2")
async def t3():
    print("t3")
```
```python
# 1.0.5 Wait for an email reply
import asyncio

async def email_reply():
    await asyncio.sleep(4)
    return (f"How you doing?")

async def task1():
    print("Waiting for reply...")
    x = await email_reply()
    print(f"Reply: {x}")

asyncio.run(task1())
```
```python
# 1.0.6 await multiple tasks
import asyncio

async def file_return():
    await asyncio.sleep(1)
    return (f"File returned")


async def email_reply():
    await asyncio.sleep(3)
    return (f"How you doing?")


async def task1():
    print("Waiting for reply...")
    x = await email_reply()
    print(f"Email Reply: {x}")


async def task2():
    print("Waiting for file...")
    x = await file_return()
    print(f"File returned: {x}")


async def main():

    # await asyncio.gather(task1(),task2())

    test = asyncio.create_task(task1())
    test2 = asyncio.create_task(task2())

    await test
    await test2

asyncio.run(main())
```


## Code Challenges
---
Use the previous code examples to help you complete the code challenges

### **Challenges**
1. Create 3 coroutines named t1, t2 and t3. Each coroutine should print out the name of the coroutine. Call/run the first coroutine and using await have t3 print out first, t2 print out second and t1 print out last.

2. Lets build a coroutine called fetch_data which simulates the collection of data from a network database. Lets assume that takes a few seconds. It should return a dictionary {"data":100}. Next, build a new coroutine which counts down from 10 to 1 (using range). Using await, have each number print to the screen every 2 seconds. Finally build a coroutine called main() and run fetch_data and the countdown coroutine concurrently. Print the data that is returned from fetch_data whilst also counting down from 10.

### Solutions
---
```Python
# Challenge 1 Solution
# async is single-threaded, single-process
import asyncio

async def t1():
    await t2()
    print("t1")

async def t2():
    print("t2")

async def t3():
    await t1()
    print("t3")

asyncio.run(t3())
```
```Python
# Challenge 2 Solution
import asyncio

async def fetch_data():
  print("Fetching data...")
  await asyncio.sleep(2)
  print("Data returned...")
  return {"data": 100}

async def task2():
  for i in range(10):
    print(i)
    await asyncio.sleep(2)

async def main():
  x = asyncio.create_task(fetch_data())
  y = asyncio.create_task(task2())

  data= await x
  print(data)
  await y

asyncio.run(main())
```