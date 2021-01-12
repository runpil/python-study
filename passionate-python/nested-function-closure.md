## 네스티드 함수와 클로저
- 네스티드 함수

    ```python
    # 네스티드 함수
    def maker(m):
        def inner(n):  # 함수 안에서 정의된 함수, nested 함수라 한다.
            return m * n
        return inner  # 위에서 정의한 nested 함수 반환

    f1 = maker(2)
    f2 = maker(3)
    f1(7)
    14
    f2(7)
    21
    ```

- 클로저 (Closure)
    - '안쪽에 위치한 네스티드 함수'가 자신이 필요한 변수의 값을 어딘가에 저장해 놓고 쓰는 테크닉

    ```python
    def maker(m):  # m은 maker 함수 안에서만 존재하는 변수
        def inner(n):
            return m * n  # maker 밖에서도 m이 유효할까?
        return inner

    f1 = maker(2)
    f2 = maker(3)
    f1(7)  # 실제 변수 m을 참조하게 되는 순간! maker 함수의 밖이다.
    14
    f2(7)
    21

    # 클로저 확인
    def maker(m):
        def inner(n):
            return m * n
        return inner

    f1 = maker(101)
    f2 = maker(75)
    f1.__closure__[0].cell_contents  # 변수 m의 값을 저장해 놓은 위치
    101
    f2.__closure__[0].cell_contents  # 변수 m의 값을 저장해 놓은 위치
    75
    ```