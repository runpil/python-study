# 정보은닉과 __dict__
- 간접 접근만 허용하는 것을 정보 은닉이라 한다.
- 정보은닉의 이점 : 객체의 안정성 높임, 새로운 기능 제공은 아니다.
- 속성 감추기

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

- 직접 접근 막는 방법

    ```python
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

- 완벽한 정보은닉

    ```python
    class Person:
        def __init__(self, n, a):
            self.__name = n  # 이름 정보
            self.__age = a  # 나이 정보
        def add_age(self, a):
            if(a < 0):
                print('나이 정보 오류')
            else:
                self.__age += a
        def __str__(self):
            return '{0}: {1}'.format(self.__name, self.__age)
        
    def main():
        p = Person('James', 22)  # 22살의 James
        #p.__age += 1  # 이 문장 실행하면 오류 발생항
        p.add_age(1)
        print(p)
        
    main()
    ```

- 약속에 근거한 코드 작성
    - 규칙 : 직접접근 허용하지 않겠다는 의미로 변수 앞에 _ 하나 붙이자.

    ```python
    class Person:
        def __init__(self, n, a):
            self._name = n  # 이름 정보
            self._age = a  # 나이 정보
        def add_age(self, a):
            if(a < 0):
                print('나이 정보 오류')
            else:
                self._age += a
        def __str__(self):
            return '{0}: {1}'.format(self._name, self._age)
        
    def main():
        p = Person('James', 22)  # 22살의 James
        #p._age += 1  # 이렇게 안 쓰기로 약속했다.
        p.add_age(1)
        print(p)
        
    main()
    James: 23
    ```

- ```__dict__```
    - 객체 내에는 해당 객체의 변수 정보를 담고 있는 딕셔너리가 하나 존재한다.
    - __dict__ 정보 출력

        ```python
        class Person:
            def __init__(self, n, a):
                self._name = n  # 이름 정보
                self._a = a  # 나이 정보

        def main():
            p = Person('James', 22)  # 22살의 James
            print(p.__dict__)  # 객체 내에 있는 딕셔너리 정보 출력
            
        main()
        {'_name': 'James', '_a': 22}
        ```

    - 객체에 변수 추가 후 ```__dict__``` 정보 출력

        ```python
        class Person:
            def __init__(self, n, a):
                self._name = n  # 이름 정보
                self._a = a  # 나이 정보

        def main():
            p = Person('James', 22)  # 22살의 James
            print(p.__dict__)
            p.len = 178  # len이라는 변수를 객체에 추가
            p.adr = 'Korea'  # adr이라는 변수를 객체에 추가
            print(p.__dict__)
            
        main()
        {'_name': 'James', '_a': 22}
        {'_name': 'James', '_a': 22, 'len': 178, 'adr': 'Korea'}
        ```

    - ```__dict__```에 접근해서 값 변경

        ```python
        class Simple:
            def __init__(self, n, s):
                self._n = n  # 단순 정수
                self._s = s  # 단순 문자열
            def __str__(self):
                return '{0}: {1}'.format(self._n, self._s)
            
        def main():
            sp = Simple(10, 'my')
            print(sp)  # __dict__ 변경 전 출력 결과
            sp.__dict__['_n'] += 10  # __dict__에 접근해서 값을 변경
            sp.__dict__['_s'] = 'your'  # __dict__에 접근해서 값을 변경
            print(sp)  # __dict__ 변경 후 출력 결과
            
        main()
        10: my
        20: your
        ```

    - 변수 이름에 언더바 두 개를 붙이면 객체 외부에서 접근 불가능한 이유
        - ```__dict__```에 등록된 속성의 이름이 다음과 같은 패턴으로 수정됨
            - 패턴 : __AttrName -> _ClassName__AttrName
            적용 : __name -> _Person__name
                        __age -> _Person__age
            - 변수 이름에 언더바를 두 개 붙이면 위의 패턴대로 이름을 바꾸어 버린다. (물론 객체 내에서는 바뀌기 이전의 이름으로 접근 가능하다.)
            - 그래서 객체 외부에서 접근이 불가능했던 것이다.

        ```python

        class Person:
            def __init__(self, n, a):
                self.__name = n  # 이름 정보
                self.__age = a  # 나이 정보
            
        def main():
            p = Person('James', 22)  # 22살의 James
            print(p.__dict__)
            
        main()
        {'_Person__name': 'James', '_Person__age': 22}
        ```