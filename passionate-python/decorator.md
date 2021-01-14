## 데코레이터
- 꾸며주는(덧붙여주는) 역할을 하는 함수 또는 클래스
- 데코레이터 예

    ```python
    def smile():  # 웃는 얼굴 출력
        print("^_^")
        
    def confused():  # 혼란스러운 얼굴 출력
        print("@_@")

    smile()
    ^_^
    confused()
    @_@

    # 데코레이터의 예
    def deco(func):  # 데코레이터 함수, 그냥 줄여서 '데코레이터'라고도 함
        def df():
            print('emotion!')  # 추가된 기능
            func()  # 원래 갖고 있던 기능
            print('emotion!')  # 추가된 기능
        return df  # 보강된 기능의 함수를 반환

    smile = deco(smile)  # smile 함수 전달하고 반환 결과를 smile에 저장
    smile()  # 기능이 보강된 smile 함수 호출
    emotion!
    ^_^
    emotion!

    confused = deco(confused)  # confused 함수 전달하고 반환 결과를 confused에 저장
    confused()  # 기능이 보강된 confused 함수 호출
    emotion!
    @_@
    emotion!
    ```

    - 기능이 추가된 새로운 함수를 만들고 이 함수를 반환한다.
- 전달 인자가 있는 함수 기반의 데코레이터

    ```python
    def adder2(n1, n2):  # 전달 인자가 두 개인 함수
        return n1 + n2

    def adder3(n1, n2, n3):  # 전달 인자가 세 개인 함수
        return n1 + n2 + n3

    adder2(3, 4)
    7
    adder3(3, 5, 7)
    15

    def adder_deco(func):  # 데코레이터 함수
        def ad(*args):  # 전달 인자를 튜플로 묶는다. (튜플 패킹)
            print(*args, sep = ' + ', end = ' ')
            print("= {0}".format(func(*args)))  # (튜플 언패킹)
        return ad

    adder2 = adder_deco(adder2)
    adder2(3, 4)
    3 + 4 = 7

    adder3 = adder_deco(adder3)
    adder3(1, 2, 3)
    1 + 2 + 3 = 6
    ```

- @ 기반으로

    ```python
    def adder_deco(func):  # 데코레이터 함수
        def ad(*args):
            print(*args, sep = ' + ', end = ' ')
            print("= {0}".format(func(*args)))
        return ad

    @adder_deco  # 아래 함수를 데코레이터 adder_deco에 통과시켜라.
    def adder2(n1, n2):  # 전달 인자가 두 개인 함수
        return n1 + n2

    @adder_deco  # 아래 함수를 데코레이터 adder_deco에 통과시켜라.
    def adder3(n1, n2, n3):  # 전달 인자가 세 개인 함수
        return n1 + n2 + n3

    def main():
        adder2(3, 4)
        adder3(3, 5, 7)
        
    main()
    3 + 4 = 7
    3 + 5 + 7 = 15
    ```

- 데코레이터 함수 두 번 이상 통과하기

    ```python
    def deco1(func):  # 데코레이터 1
        def inner():
            print('deco1')
            func()
        return inner

    def deco2(func):  # 데코레이터 2
        def inner():
            print('deco2')
            func()
        return inner

    @deco1
    @deco2
    def simple():
        print('simple')
        
    def main():
        simple()
        
    main()
    deco1
    deco2
    simple
    ```