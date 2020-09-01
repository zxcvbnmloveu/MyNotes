# `使用argparse调参`

```python3
import argparse
#导入包
parser = argparse.ArgumentParser(description='Conditional Domain Adversarial Network')
#定义，声明
parser.add_argument('-a', '--apple', type=int, default=10)
parser.add_argument('-s', type=str, help='this is a string')
#指定参数，类型和描述
args = parser.parse_args()
#获取一个字典
print(vars(args))
#输出{'apple':12, 's':'hello'}

```
