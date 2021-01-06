## isinstance 함수와 object 클래스
- isinstance(object, classinfo) : 객체의 클래스 유형을 확인하는 함수

    ```python
    # ex1
    class Simple:
        pass  # 빈 클래스를 정의하는 방법

    s = Simple()
    isinstance(s, Simple)  # s가 Simple 클래스의 객체인가?
    True

    # ex2
    isinstance([1, 2], list) # [1, 2]가 list 클래스의 객체인가?
    True

    # ex3
    class Fruit():
        pass

    class Apple(Fruit):  # Fruit을 상속하는 Apple
        pass

    class SuperApple(Apple):  # Apple을 상속하는 SuperApple
        pass

    sa = SuperApple()
    isinstance(sa, SuperApple)
    True

    isinstance(sa, Apple)
    True

    isinstance(sa, Fruit)
    True
    ```

    - SuperApple 클래스는 Apple 클래스를 직접 상속한다.
    - SuperApple 클래스는 Apple을 상속함으로써 Fruit 클래스를 간접 상속한다.
- object 클래스
    - 파이썬의 모든 클래스는 object 클래스를 직접 혹은 간접 상속한다.

    ```python
    # ex1
    class Simple:  # 아무것도 상속하지 않으면 object 클래스를 상속하게 된다.
        pass

    isinstance(Simple(), object)  # Simple 객체가 object 클래스를 상속하는가?
    True

    isinstance([1, 2], object)  # 리스트는 object 클래스를 상속하는가?
    True

    # ex2
    class A:  # 아무것도 상속하지 않으므로 object 클래스 상속!
        pass

    class Z(A):  # Z는 A를 상속한다. 따라서 z는 object 클래스를 간접 상속!
        pass

    issubclass(Z, A)  # Z는 A를 상속하는가?
    True

    issubclass(type, object)  # type 클래스는 object 클래스를 상속하는가?
    True

    dir(object)  # object 클래스에 있는 메소드와 변수들을 보여라.
    ['__class__',
        '__delattr__',
        '__dir__',
        '__doc__',
        '__eq__',
        '__format__',
        '__ge__',
        '__getattribute__',
        '__gt__',
        '__hash__',
        '__init__',
        '__init_subclass__',
        '__le__',
        '__lt__',
        '__ne__',
        '__new__',
        '__reduce__',
        '__reduce_ex__',
        '__repr__',
        '__setattr__',
        '__sizeof__',
        '__str__',
        '__subclasshook__']
    ```