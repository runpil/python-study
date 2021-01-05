## 클래스와 객체의 본질
- 클래스 : 객체를 만들기 위한 일종의 설계도
- 객체 : 클래스를 기반으로 만들어진 실제 사물
- 클래스 예

    ```python
    class Simple:
        def seti(self, i):  # seti 메소드의 정의
            self.i = i
        def geti(self):  # geti 메소드의 정의
            return self.i

    s1 = Simple()
    s1.seti(200)  # 이 메소드의 실행 과정에서 객체 내에 변수 i가 만들어진다.
    s1.geti()
    200

    s2 = Simple()
    s2.geti()  # 아직 객체 내에 변수 i가 없는 상태이므로 오류 발생!
    ---------------------------------------------------------------------------
    AttributeError                            Traceback (most recent call last)
    <ipython-input-5-a842b52f6d5b> in <module>
            1 s2 = Simple()
    ----> 2 s2.geti()  # 아직 객체 내에 변수 i가 없는 상태이므로 오류 발생!

    <ipython-input-1-d350cbe3c7dd> in geti(self)
            3         self.i = i
            4     def geti(self):  # geti 메소드의 정의
    ----> 5         return self.i

    AttributeError: 'Simple' object has no attribute 'i'
    ```

- 클래스를 디자인하는 모범적인 형태
    - __init__ 메소드를 잘 정의하는 것(모든 변수를 적절히 초기화하는 것)이 중요하다.

    ```python
    class Simple:
        def __init__(self):  # 자동으로 호출되는 메소드
            self.i = 0  # 변수 초기화, 이 순간에 변수 i가 만들어짐
        def seti(self, i):
            self.i = i
        def geti(self):
            return self.i

    s = Simple()
    s.geti()
    0

    s.seti(25)
    s.geti()
    25
    ```

- 객체에 변수와 메소드 붙였다 떼었다 해보기

    ```python
    class SoSimple:
        def geti(self):
            return self.i

    ss = SoSimple()
    ss.i = 27  # 이 순간 변수 ss에 담긴 객체에 i라는 변수가 생긴다.
    ss.geti()  # ss에 담긴 객체에 i가 생겼으므로 geti 메소드 호출 가능
    27

    ss.hello = lambda : print('hi~')  # hello라는 메소드를 추가
    ss.hello()
    hi~

    del ss.i  # ss에 담긴 객체에서 변수 i 삭제
    ss.geti()
    ---------------------------------------------------------------------------
    AttributeError                            Traceback (most recent call last)
    <ipython-input-16-8ad3603dae45> in <module>
    ----> 1 ss.geti()

    <ipython-input-10-314f59bea353> in geti(self)
            1 class SoSimple:
            2     def geti(self):
    ----> 3         return self.i

    AttributeError: 'SoSimple' object has no attribute 'i'
    ```

- 클래스에 변수 추가하기

    ```python
    class Simple:
        def __init__(self, i):
            self.i = i
        def geti(self):
            return self.i

    Simple.n = 7  # Simple 클래스에 변수 n을 추가하고 7로 초기화
    Simple.n
    7

    s1 = Simple(3)
    s2 = Simple(5)
    print(s1.n, s1.geti(), sep = ', ')
    7, 3
    print(s2.n, s2.geti(), sep = ', ')
    7, 5
    ```

    - 클래스에 속하는 변수를 만들 수 있다. (클래스도 객체이기 때문에)
    - 객체에 '찾는 변수'가 없으면 해당 객체의 클래스로 찾아가서 그 변수를 찾는다.
- 파이썬에서는 클래스도 객체이다.

    ```python
    # type은 자료형을 확인할 때 호출해 왔던 함수의 이름
    # 이는 사실 클래스의 이름이다.
    type
    <class 'type'>

    class Simple:
        pass  # 텅 빈 클래스를 만드는 방법!
    type(Simple)  # Simple 클래스 전달하는 상황
    <class 'type'>

    # 클래스도 객체이다.
    # 클래스는 type이라는 클래스의 객체이다.
    simple2 = Simple  # 변수 simple2에 클래스 Simple 담음
    s1 = Simple()  # 클래스 Simple로 객체 생성
    s2 = simple2()  # 변수 simple2로도 객체 생성할 수 있음
    ```