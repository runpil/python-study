## 정보은닉과 ```__dict__```
- 간접 접근만 허용하는 것을 정보 은닉이라 한다.
- 정보은닉의 이점 : 객체의 안정성 높임, 새로운 기능 제공은 아니다.

```python
class Person:
    def __init__(self, n, a):
        self.name = n  # 이름 정보
        self.age = a  # 나이 정보
    def __str__(self):
        return '{0}: {1}'.format(self.name, self.age)
    
def main():
    p = Person('James', 22)  # 22살의 James
    print(p)
    p.age -= 1  # 나이 한 살 더 먹어서 넣은 문장, 실수가 있는 문장
    print(p)
    
main()
James: 22
James: 21

# 직접 접근 허용 원치 않음
class Person:
    def __init__(self, n, a):
        self.name = n  # 이름 정보
        self.age = a  # 나이 정보
    def add_age(self, a):
        if(a < 0):  # 입력에 오류가 있다면,
            print('나이 정보 오류')
        else:  # 입력이 정상적이라면,
            self.age += a
    def __str__(self):
        return '{0}: {1}'.format(self.name, self.age)
    
def main():
    p = Person('James', 22)  # 22살의 James
    p.add_age(1)
    print(p)
    
main()
James: 23
```