## 불과 비교, 논리 연산자 알아보기

### 비교 연산자의 판단 결과
- 파이썬에서는 비교 연산자와 논리 연산자의 판단 결과로 True, False를 사용한다.
- 비교 결과가 맞으면 True 아니면 False
```
>>> 3 > 1
True
```

### 숫자가 같은지 다른지 비교하기
```
>>> 10 == 10
True
>>> 10 != 5
True
```

### 문자열이 같은지 다른지 비교하기
- 단어가 같아도 대소문자가 다르면 다른 문자열로 판단한다.
```
>>> 'Python' == 'Python'
True
>>> 'Python' == 'python'
False
>>> 'Python' != 'python'
True
```

### 부등호 사용하기
```
>>> 10 > 20
False
>>> 10 < 20
True
>>> 10 >= 10
True
>>> 10 <= 10
True
```

### 객체가 같은지 다른지 비교하기
- is, is not은 객체(object)를 비교한다.
```
>>> 1 == 1.0
True
>>> 1 is 1.0
False
>>> 1 is not 1.0
True
```

### 정수 객체와 실수 객체가 서로 다른지 확인하는 방법
- id 함수는 객체의 고유한 값(메모리 주소)을 구하며 이 값은 파이썬을 실행하는 동안 계속 유지되며 다시 실행하면 달라진다.
```
>>> id(1)
1802225392
>>> id(1.0)
2221640721344
```

### 논리 연산자 사용하기
```
a and b
>>> True and True
True
>>> True and False
False
>>> False and True
False
>>> False and False
False

a or b
>>> True or True
True
>>> True or False
True
>>> False or True
True
>>> False or False
False

not x
>>> not True
False
>>> not False
True
```

### 논리 연산자와 비교 연산자 함께 사용하기
- 비교 연산자(is, is not, ==, !=, <, >, <=, >=)를 먼저 판단하고 논리 연산자(not, and, or)를 판단한다.
```
>>> 10 == 10 and 10 != 5
True
>>> 10 > 5 or 10 < 3
True
>>> not 10 > 5
False
>>> not 1 is 1.0
True
```
