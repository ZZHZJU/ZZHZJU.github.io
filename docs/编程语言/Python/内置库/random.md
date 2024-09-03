# Random
Python 的 `random` 模块用于生成随机数和进行随机选择操作。

### 1. 生成随机浮点数
- `random.random()`: 生成一个 0 到 1 之间的随机浮点数（不包括 1）。
  
  ```python
  import random
  print(random.random())  # 输出类似于 0.37444887175646646 的值
  ```

- `random.uniform(a, b)`: 生成一个范围在 `a` 到 `b` 之间的随机浮点数。

  ```python
  print(random.uniform(1.5, 6.5))  # 输出类似于 4.563342826192823 的值
  ```

### 2. 生成随机整数
- `random.randint(a, b)`: 生成一个范围在 `a` 到 `b` 之间的随机整数（包括 `a` 和 `b`）。

  ```python
  print(random.randint(1, 10))  # 输出类似于 7 的值
  ```

- `random.randrange(start, stop[, step])`: 生成一个在 `start` 和 `stop` 之间（不包括 `stop`）按 `step` 增加的随机整数。

  ```python
  print(random.randrange(0, 100, 5))  # 输出类似于 25 的值
  ```

### 3. 随机选择
- `random.choice(seq)`: 从序列 `seq` 中随机选择一个元素。

  ```python
  items = ['apple', 'banana', 'cherry']
  print(random.choice(items))  # 输出类似于 'banana' 的值
  ```

- `random.choices(population, weights=None, k=1)`: 从 `population` 中随机选择 `k` 个元素，返回包含 `k` 个元素的列表。可以通过 `weights` 指定各元素的选择概率。

  ```python
  items = ['apple', 'banana', 'cherry']
  print(random.choices(items, weights=[10, 1, 1], k=2))  # 可能输出 ['apple', 'banana']
  ```

- `random.sample(population, k)`: 从 `population` 中随机选择 `k` 个不同的元素，返回包含 `k` 个元素的列表。

  ```python
  print(random.sample(range(100), 5))  # 可能输出 [36, 17, 97, 23, 58]
  ```

### 4. 打乱顺序
- `random.shuffle(seq)`: 就地打乱序列 `seq` 的顺序。

  ```python
  items = [1, 2, 3, 4, 5]
  random.shuffle(items)
  print(items)  # 可能输出 [3, 1, 4, 5, 2]
  ```

### 5. 随机种子
- `random.seed(a=None)`: 初始化随机数生成器。如果指定了 `a`，随机数生成器将以 `a` 为种子，这样每次运行代码生成的随机数都是一样的。

  ```python
  random.seed(10)
  print(random.random())  # 输出总是相同的值
  ```