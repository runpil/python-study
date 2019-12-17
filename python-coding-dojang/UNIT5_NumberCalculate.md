## 숫자 계산하기
### 사칙연산
```
# 덧셈
>>> 1 + 1
2

# 뺄셈
>>> 1 - 2
-1

# 곱셈
>>> 2 * 2
4

# 나눗셈
>>> 5 / 2
2.5
>>> 4 / 2
2.0
※ 파이썬3는 정수끼리 나눗셈을 해도 실수가 나온다.
```

### 나눗셈 후 소수점 이하를 버리는 // 연산자
- //은 버림 나눗셈(floor division)이라고 부르며 나눗셈의 결과에서 소수점 이하는 버린다.
```
>>> 5 // 2
2
>>> 4 // 2
2

※ 실수에 // 연산자를 사용하면 결과는 실수가 나오며 소수점 이하는 버린다.
>>> 5.5 // 2
2.0
>>> 4 // 2.0
2.0
>>>4.1 // 2.1
1.0
```

### 나눗셈 후 나머지를 구하는 % 연산자
- 두 수를 나누었을 때 나머지만 구하며 모듈로(modulo) 연산자라고 부른다.
```
>>> 5 % 2
1
```

### 몫과 나머지 함께 구하기
```
>>> divmod(5, 2)
(2, 1)

>>> quotient, remainder = divmod(5, 2)
>>> print(quotient, remainder)
2 1
```

### 거듭제곱을 구하는 ** 연산자
- 숫자를 특성 횟수만큼 곱한다.
```
>>> 2 ** 10
1024
```

### 값을 정수로 만들기
- int에 괄호를 붙이고 숫자 또는 계산식을 넣으면 된다.
```
>>> int(3.3)
3
>>> int(5 / 2)
2
>>> int('10')
10
```

### 객체의 자료형 알아내기
```
>>> type(10)
<class'int'>
>>> type(3.5)
<class 'float'>
```

### 2진수, 8진수, 16진수
- 2진수 : 숫자 앞에 0b를 붙이며 0과 1을 사용한다.
- 8진수 : 숫자 앞에 0o를 붙이며 0부터 7까지 사용한다.
- 16진수 : 숫자 앞에 0x를 붙이며 0부터 9, A부터 F까지 사용한다.(소문자 a부터 f도 가능)
```
>>> 0b110
6
>>> 0o10
8
>>> 0xF
15
```

### 값을 실수로 만들기
- float에 괄호를 붙이고 숫자 또는 계산식을 넣으면 된다.
```
>>> float(5)
5.0
>>> float(1 + 2)
3.0
>>> float('5.3')
5.3
```
