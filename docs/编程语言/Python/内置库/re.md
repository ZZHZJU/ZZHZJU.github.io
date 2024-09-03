# RE
Python 的 `re` 库是一个用于正则表达式匹配操作的库。它提供了多种功能来处理字符串模式匹配、查找和替换等操作。以下是一些 `re` 库常用的函数和方法：

### 1. `re.match()`
`re.match()` 尝试从字符串的起始位置匹配一个模式。如果匹配成功，它将返回一个匹配对象；否则返回 `None`。

```python
import re

pattern = r'\d+'
string = '123abc456'
match = re.match(pattern, string)

if match:
    print(f"匹配成功: {match.group()}")
else:
    print("匹配失败")
```

### 2. `re.search()`
`re.search()` 在整个字符串中搜索第一个匹配的模式，如果找到则返回一个匹配对象。

```python
import re

pattern = r'\d+'
string = 'abc123def456'
match = re.search(pattern, string)

if match:
    print(f"匹配成功: {match.group()}")
else:
    print("匹配失败")
```

### 3. `re.findall()`
`re.findall()` 返回字符串中所有非重叠模式的匹配项，作为一个列表。

```python
import re

pattern = r'\d+'
string = 'abc123def456'
matches = re.findall(pattern, string)
print(f"所有匹配项: {matches}")
```

### 4. `re.sub()`
`re.sub()` 用于替换字符串中每一个匹配正则表达式模式的子串，并返回替换后的字符串。

```python
import re

pattern = r'\d+'
replacement = '#'
string = 'abc123def456'
new_string = re.sub(pattern, replacement, string)
print(f"替换后的字符串: {new_string}")
```

### 5. `re.split()`
`re.split()` 按照能够匹配的子串将字符串分割后返回列表。

```python
import re

pattern = r'\d+'
string = 'abc123def456'
split_string = re.split(pattern, string)
print(f"分割后的字符串列表: {split_string}")
```

### 6. `re.compile()`
`re.compile()` 可以将正则表达式模式编译成一个正则表达式对象，以提高匹配的效率，特别是在需要重复使用相同模式时。

```python
import re

pattern = r'\d+'
compiled_pattern = re.compile(pattern)
matches = compiled_pattern.findall('abc123def456')
print(f"编译模式后的匹配项: {matches}")
```

### 常用的正则表达式符号
- `.`: 匹配任意字符（除了换行符）
- `^`: 匹配字符串的开头
- `$`: 匹配字符串的结尾
- `*`: 匹配前一个字符零次或多次
- `+`: 匹配前一个字符一次或多次
- `?`: 匹配前一个字符零次或一次
- `\d`: 匹配任何数字
- `\w`: 匹配任何字母数字字符或下划线
- `[abc]`: 匹配括号内的任意一个字符