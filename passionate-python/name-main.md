## __name__ & __main__
- ```__name__```
    - 파이썬 스크립트 파일을 실행하면 자동으로 생성되는 변수
- 실행이 시작되는 스크립트 파일의 __name__에는 문자열 '```__main__```'을 채운다.

    ```python
    # who_are_you.py
    def main():
        print('file name: who_are_you.py')
        print('__name__: {0}'.format(__name__))  # 변수 __name__의 출력

    main()

    file name: who_are_you.py
    __name__: __main__
    ```

- import 되는 스크립트 파일의 ```__name__```에는 파일 이름을 문자열로 채운다.

    ```python
    # importer.py
    import who_are_you  # who_are_you.py를 import
    print('play importer')
    print('__name__: {0}'.format(__name__))

    file name: who_are_you.py
    __name__: who_are_you
    play importer
    __name__: __main__
    ```

- if ```__name__``` == '```__main__```'
    - 파이썬의 스크립트 파일에 담기는 내용은 다음과 같이 두 가지로 나눌 수 있다.
        - 직접 실행할 내용이거나,
        - 아니면 다른 스크립트 파일에서 사용하도록 만든 내용이거나
    - 다른 스크립트 파일에서 가져다 쓰지 못하는 경우

        ```python
        # adder.py
        def add(n1, n2):
            return n1 + n2

        def main():  # 이 파일을 import 하면 main 함수도 정의됨
            print(add(3, 4))
            print(add(5, 9))
            
        main()  # 이 파일을 import 하면 이 문장에 의해 main 함수도 실행됨

        7
        14
        ```

    - 다른 파일에서 import해서 add 함수를 호출할 수 있게 작성
        - adder2.py를 직접 실행해야만 main() 함수가 호출된다.

        ```python
        # adder2.py
        def add(n1, n2):
            return n1 + n2

        if __name__ == '__main__':
            def main():  # if의 조건이 True인 경우에만 main 함수가 정의된다.
                print(add(3, 4))
                print(add(5, 9))
                
            main()  # if의 조건이 True인 경우에만 main 함수가 호출된다.

        7
        14
        ```

    - import 해서 add 함수 호출하기

        ```python
        # divider.py
        import adder2 as ad  # adder2.py를 import

        def divide(n1, n2):
            return n1 / n2

        def main():
            print(divide(4, 2))
            print(divide(9, 3))
            print(ad.add(2, 3))  # adder2.py에 정의된 add 함수 호출
            
        main()

        2.0
        3.0
        5
        ```