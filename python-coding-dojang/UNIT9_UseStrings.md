## 문자열 사용하기

### 문자열 안에 작은따옴표나 큰따옴표 포함하기
- 문자열 안에 '(작은따옴표)를 넣고 싶다면 문자열을 "(큰따옴표)로 묶어준다.
- 문자열 안에 "(큰따옴표)를 넣고 싶다면 문자열을 '(작은따옴표)로 묶어준다.
- 작은 따옴표 안에 작은따옴표를 넣거나 큰따옴표 안에 큰따옴표를 넣을 수 없다.
```
>>> s = "Pyton isn't difficult"
>>> s
"Python isn't difficult"

>>> s = 'He said "Python is easy"'
>>> s
'He said "Python is easy"'

>>> s = 'Python isn't difficult'
SyntaxError: invalid syntax
>>> s = "He said "Python is easy""
SyntaxError: invalid syntax
```
- 여러 줄로 된 문자열은 작은따옴표 안에 작은따옴표와 큰따옴표를 둘 다 넣을 수 있다.
```
single_quote = '''"안녕하세요."
'파이썬'입니다.'''

double_quote1 = """"Hello"
'Python'"""

double_quote2 = """Hello, 'Python'"""

print(single_quote)
print(double_quote1)
print(double_quote2)
```

### 문자열에 따옴표를 포함하는 다른 방법
- 따옴표 앞에 \(역슬래시)를 붙이면 된다.
```
>>> 'Python isn\'t difficult'
"Python isn'tdifficult"
```

### 따옴표 세 개로 묶지 않고 여러 줄로 된 문자열 사용하기
- 문자열 안에 개행 문자(\n)를 넣으면 여러 줄로 된 문자열을 사용할 수 있다.
```
>>> print('Hello\nPython')
Hello
Python
```


