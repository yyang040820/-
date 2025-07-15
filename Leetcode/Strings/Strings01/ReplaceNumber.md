## 54. 替换数字（第八期模拟笔试）

题目描述:
给定一个字符串 s，它包含小写字母和数字字符，请编写一个函数，将字符串中的字母字符保持不变，而将每个数字字符替换为number。 例如，对于输入字符串 "a1b2c3"，函数应该将其转换为 "anumberbnumbercnumber"。

输入描述

输入一个字符串 s,s 仅包含小写字母和数字字符。

输出描述

打印一个新的字符串，其中每个数字字符都被替换为了number

输入示例

a1b2c3

输出示例

anumberbnumbercnumber

提示信息

数据范围：

1 <= s.length < 10000。

#### 简易回答
遍历字符串，如果是小写字母就保留；如果是数字字符（digit），就用字符串 `"number"` 进行替换。

---
#### 详细回答
这是一个典型的字符串处理问题，思路如下：

1. 逐字符遍历输入字符串；
2. 遇到小写字母时，原样保留；
3. 遇到数字字符（如 `'0'`~`'9'`），立即替换为 `"number"`；
4. 注意：无需将连续数字组合成一个完整数字，只要出现一个数字字符就立即替换；
5. 最终将结果拼接输出。

---

```python
import sys
input = sys.stdin.read
def main():
    data = input().split()
    index = 0
    input_str = data[index]

    replace = 'number'
    res = ''

    for ch in input_str:
        if ch.islower():
            res += ch
        elif ch.isdigit():
            res += replace

    print(res)
    

if __name__ == "__main__":
    main()
```
