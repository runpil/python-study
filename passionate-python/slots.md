## ```__slots__```의 효과
- ```__dict__```의 단점
    - 딕셔너리는 리스트나 튜플에 비해서 메모리 사용량이 많다.
    - '키'를 이용해서 '값'을 바로 얻을 수 있도록 하기 위해서 파이썬이 더 많은 정보를 유지하기 때문이다.
    - 따라서 많은 수의 객체를 생성해야 하는 경우에는 객체 하나당 하나씩 존재하는 ```__dict__```의 존재가 부담이 된다.

    ```python
    class Point3D:
        def __init__(self, x, y, z):
            self.x = x  # x 좌표
            self.y = y  # y 좌표
            self.z = z  # z 좌표
        def __str__(self):
            return '({0}, {1}, {2})'.format(self.x, self.y, self.z)  # 좌표 정보 출력
        
    def main():
        p1 = Point3D(1, 1, 1)  # 3차원 좌표상 한 점
        p2 = Point3D(24, 17, 31)  # 3차원 좌표상 한 점
        print(p1)
        print(p2)
        
    main()
    (1, 1, 1)
    (24, 17, 31)
    ```

- ```__slots__```의 사용
    - ```__slots__``` = ('x', 'y', 'z') 가 의미하는 바는 다음과 같다.
        - "이 클래스를 기반으로 생성한 객체의 변수는 x, y, z,로 제한한다."

    ```python
    class Point3D:
        __slots__ = ('x', 'y', 'z')  # 속성을(변수를) x, y, z로 제한한다!
        
        def __init__(self, x, y, z):
            self.x = x  # x 좌표
            self.y = y  # y 좌표
            self.z = z  # z 좌표
        def __str__(self):
            return '({0}, {1}, {2})'.format(self.x, self.y, self.z)  # 좌표 정보 출력
        
    def main():
        p1 = Point3D(1, 1, 1)  # 3차원 좌표상 한 점
        p2 = Point3D(24, 17, 31)  # 3차원 좌표상 한 점
        print(p1)
        print(p2)
        
    main()
    (1, 1, 1)
    (24, 17, 31)
    ```
- ```__slots__``` 유무에 따른 속도 비교
    - 파이썬 시간 측정 방법

        ```python
        import timeit

        start = timeit.default_timer()  # 시작
        # 실행 속도를 측정하고자 하는 내용을 여기에 담음
        stop = timeit.default_timer()  # 끝
        print(stop - start)  # 걸린 시간 확인
        1.8584999907034216e-05
        ```

    - ```__slots__ ```없는 경우

        ```python
        import timeit  # 시간 측정을 위한 모듈

        class Point3D:
            def __init__(self, x, y, z):
                self.x = x  # x 좌표
                self.y = y  # y 좌표
                self.z = z  # z 좌표
            def __str__(self):
                return '({0}, {1}, {2})'.format(self.x, self.y, self.z)
            
        def main():
            start = timeit.default_timer()
            p = Point3D(1, 1, 1)
            
            for i in range(3000):
                for i in range(3000):
                    p.x += 1
                    p.y += 1
                    p.z += 1
            print(p)
            
            stop = timeit.default_timer()
            print(stop - start)  # 실행에 걸린 속도 계산 및 출력
                  
        main()
        (9000001, 9000001, 9000001)
        2.298747684999853
        ```

    - ```__slots__``` 있는 경우

        ```python
        import timeit  # 시간 측정을 위한 모듈

        class Point3D:
            __slots__ = ('x', 'y', 'z')
            
            def __init__(self, x, y, z):
                self.x = x  # x 좌표
                self.y = y  # y 좌표
                self.z = z  # z 좌표
            def __str__(self):
                return '({0}, {1}, {2})'.format(self.x, self.y, self.z)
            
        def main():
            start = timeit.default_timer()
            p = Point3D(1, 1, 1)
            
            for i in range(3000):
                for i in range(3000):
                    p.x += 1
                    p.y += 1
                    p.z += 1
            print(p)
            
            stop = timeit.default_timer()
            print(stop - start)  # 실행에 걸린 속도 계산 및 출력
                  
        main()
        (9000001, 9000001, 9000001)
        2.1330743260000418
        ```