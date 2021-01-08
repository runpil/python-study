## 연산자 오버로딩
- 오버로딩 예시

    ```python
    class Account:  # 계좌 클래스
        def __init__(self, aid, abl):
            self.aid = aid  # 계좌 번호
            self.abl = abl  # 계좌 잔액
        def __add__(self, m):  # 입금
            self.abl += m
            print('__add__')
        def __sub__(self, m):  # 출금
            self.abl -= m
            print('__sub__')
        def __call__(self):  # 계좌 상황을 문자열로 반환
            print('__call__')
            return str(self.aid) + ':' + str(self.abl)
        
    def main():
        acnt = Account('James01', 100)  # 계좌 개설
        acnt + 100  # 100원 입금, __add__ 호출로 이어짐
        acnt - 50  # 50원 출금, __sub__ 호출로 이어짐
        print(acnt())  # 계좌 정보 확인, __call__ 호출로 이어짐
        
    main()
    __add__
    __sub__
    __call__
    James01:150
    ```

- 적절한 형태로 +와 - 연산자 오버로딩

    ```python
    n1 = 3
    n2 = 5
    n1 + n2  # + 결과로 새로운 정수가 만들어짐, n1과 n2는 그대로임
    **8

    s1 = 'Y'
    s2 = 'oon'
    s1 + s2  # + 결과로 새로운 문자열 만들어짐, s1과 s2는 그대로임
    'Yoon'

    class Vector:  # 벡터를 표현한 클래스
        def __init__(self, x, y):
            self.x = x  # 벡터의 x 방향 값
            self.y = y  # 벡터의 y 방향 값
        def __add__(self, o):  # 벡터의 덧셈 연산
            return Vector(self.x + o.x, self.y + o.y)  # 새로운 객체 생성 및 반환
        def __call__(self):  # 벡터 정보를 문자열로 반환
            return 'Vector({0}, {1})'.format(self.x, self.y)
        
    def main():
        v1 = Vector(3, 3)
        v2 = Vector(7, 7)
        v3 = v1 + v2  # 새로운 Vector 객체 생성되어 v3에 저장
        print(v1())  # __call__ 호출 결과로 반환되는 문자열 출력
        print(v2())  # __call__ 호출 결과로 반환되는 문자열 출력
        print(v3())  # __call__ 호출 결과로 반환되는 문자열 출력

    main()
    Vector(3, 3)
    Vector(7, 7)
    Vector(10, 10)**
    ```

- 메소드 __str__의 정의

    ```python
    class Simple:
        def __init__(self, i):
            self.i = i

    s = Simple(10)  # 10이 저장된 Simple 객체 생성
    print(s)
    <__main__.Simple object at 0x7fe7430a5ad0>

    s.__str__()  # object 클래스의 __str__ 메소드 호출
    '<__main__.Simple object at 0x7fe7430a5ad0>'

    class Simple:
        def __init__(self, i):
            self.i = i
        def __str__(self):
            return 'Simple({0})'.format(self.i)  # 'Simpe(20)' 형태의 문자열 생성 및 반환

    s = Simple(20)
    print(s)  # __str__ 메소드가 반환하는 문자열 출력
    Simple(20)

    class Vector:  
        def __init__(self, x, y):
            self.x = x  
            self.y = y  
        def __add__(self, o):  # 벡터의 덧셈 연산
            return Vector(self.x + o.x, self.y + o.y)  
        def __str__(self):  # 벡터 정보를 문자열로 반환
            return 'Vector({0}, {1})'.format(self.x, self.y)
        
    def main():
        v1 = Vector(3, 3)
        v2 = Vector(7, 7)
        v3 = v1 + v2
        print(v1)  # __str__ 호출 결과로 반환되는 문자열 출력
        print(v2)  # __str__ 호출 결과로 반환되는 문자열 출력
        print(v3)  # __str__ 호출 결과로 반환되는 문자열 출력

    main()
    Vector(3, 3)
    Vector(7, 7)
    Vector(10, 10)
    ```

- in-place 형태의 연산자 오버로딩

    ```python
    # immutable 객체를 대상으로 += 연산
    # 정수와 문자열은 수정 불가능한 immutable 객체이다.
    n = 5
    id(n)  # 5가 저장된 위치
    4335801136
    n += 1
    id(n)  # += 연산 이후에 달라진 위치
    4335801168

    # mutable 객체를 대상으로 += 연산
    n = [1, 2]
    id(n)  # 리스트 [1, 2]가 저장된 위치
    140631240816192
    n += [3]
    id(n)  # += 연산 후에도 위치가 달라지지 않았다.
    140631240816192

    class Vector:
        def __init__(self, x, y):
            self.x = x
            self.y = y
        def __add__(self, o):  # 백터의 + 연산
            return Vector(self.x + o.x, self.y + o.y)  # 새로운 객체 생성 및 반환
        def __iadd__(self, o):  # 백터의 += 연산
            self.x += o.x
            self.y += o.y
            return self  # v1 += v2의 연산 결과로 v1을 반환, 꼭 넣어줘야 함
        def __str__(self):  # 벡터 정보를 문자열로 반환
            return 'Vector({0}, {1})'.format(self.x, self.y)
        
    def main():
        v1 = Vector(2, 2)
        v2 = Vector(7, 7)
        print(v1, id(v1))  # v1과 v1에 저장된 객체의 주소 정보 출력
        v1 += v2  # v1 = v1.__iadd__(v2)
        print(v1, id(v1))  # v1과 v1에 저장된 객체의 주소 정보 출력
        
    main()
    Vector(2, 2) 140631240906960
    Vector(9, 9) 140631240906960
    ```