## 클래스 메소드와 static 메소드
- 인스턴스 변수
    - 첫 대입 연산에서 생성되는 변수를 가리켜 '인스턴스 변수'라 한다. 그리고 이는 각 객체별로 존재한다. 그러니까 '이는 객체에 속한 변수'이다.

        ```python
        class Simple:
            def __init__(self):
                self.iv = 10  # iv는 인스턴스 변수, 객체별로 존재하는 변수
                
        s = Simple()
        s.iv  # 인스턴스 변수는 객체를 통해서 접근을 한다.
        10
        ```

- 클래스 변수
    - 변수를 클래스 안에 둘 수 있다. 변수는 클래스에 속하는 '클래스 변수'가 된다.

    ```python
    class Simple:
        cv = 20  # cv는 클래스 변수, 클래스 Simple에 속하는 변수
        def __init__(self):
            self.iv = 10
            
    Simple.cv  # 클래스 변수는 클래스 이름으로 접근 가능
    20
    s = Simple()
    s.cv  # 클래스 변수는 객체를 통해서도 접근 가능
    20
    s.iv
    10
    ```

- 클래스 변수 활용

    ```python
    class Simple:
        count = 0  # Simple의 클래스 변수, 생성된 객체 수를 저장하는 것이 목적
        def __init__(self):
            Simple.count += 1  # 클래스 변수 count 값 1 증가
        def get_count(self):
            return Simple.count  # 클래스 변수 count 값 반환
        
    def main():
        s1 = Simple()  # 클래스 변수 count의 값은 1이 된다.
        print(s1.get_count())  # s1의 메소드 호출
        s2 = Simple()  # 클래스 변수 count의 값은 2가 된다.
        print(s1.get_count())  # 이번에도 s1의 메소드 호출
        s3 = Simple()  # 클래스 변수 count의 값은 3이 된다.
        print(s1.get_count())  # 마지막에도 s1의 메소드 호출
        
    main()
    1
    2
    3
    ```

- static 메소드
    - 클래스에 속하는 메소드 (객체가 없어도 언제든지 호출 가능한 메소드)
    - 생성 방법 1

        ```python
        class Simple:
            def sm():  # static 메소드는 첫 번째 인자로 self가 없다!
                print('static method!')
            sm = staticmethod(sm)  # sm 메소드를 static 메소드로 만드는 방법이다.

        def main():
            Simple.sm()  # static 메소드는 클래스 이름을 통해 호출 가능
            s = Simple()
            s.sm()  # static 메소드는 객체를 통해서도 호출 가능
            
        main()
        static method!
        static method!
        ```

    - 생성 방법 2 (권장)

        ```python
        class Simple:
            count = 0
            def __init__(self):
                Simple.count += 1
                
            @staticmethod  # 아래의 메소드를 static 메소드로 선언!
            def get_count():  # 매개변수로 self가 없는 static 메소드
                return Simple.count
            
        def main():
            print(Simple.get_count())  # 객체가 없는 상태에서도 객체의 수를 물을 수 있다.
            s = Simple()
            print(Simple.get_count())
            
        main()
        0
        1
        ```

- class 메소드
    - static 메소드와 상당히 유사한 메소드
    - 예시 1

        ```python
        class Simple:
            num = 5  # 클래스 변수
            @staticmethod
            def sm(i):  # static 메소드
                print('st~ 5 + {0} = {1}'.format(i, Simple.num + i))
            @classmethod
            def cm(cls, i):  # class 메소드
                print('cl~ 5 + {0} = {1}'.format(i, Simple.num + i))
                
        def main():
            Simple.sm(3)  # 클래스 이름 기반의 static 메소드 호출
            Simple.cm(3)  # 클래스 이름 기반의 class 메소드 호출
            s = Simple()
            s.sm(4)  # 객체를 대상으로 한 static 메소드 호출
            s.cm(4)  # 객체를 대상으로 한 class 메소드 호출
            
        main()
        st~ 5 + 3 = 8
        cl~ 5 + 3 = 8
        st~ 5 + 4 = 9
        cl~ 5 + 4 = 9
        ```

    - 예시 2

        ```python
        class Simple:
            count = 0  # 생성된 객체의 수
            def __init__(self):
                Simple.count += 1
            @classmethod
            def get_count(cls):
                return cls.count  # cls에 전달되는 것은 Simple 클래스
            
        def main():
            print(Simple.get_count())
            s = Simple()
            print(Simple.get_count())
            
        main()
        0
        1
        ```

    - 예시 3

        ```python
        class Natural:
            def __init__(self, n):
                self.n = n
            def getn(self):
                return self.n
            @classmethod
            def add(cls, n1, n2):
                return cls(n1.getn() + n2.getn())  # Natural 객체 생성 후 반환
            
        def main():
            n1 = Natural(1)
            n2 = Natural(2)
            n3 = Natural.add(n1, n2)  # 반환되는 객체를 n3에 저장
            print('{0} + {1} = {2}'.format(n1.getn(), n2.getn(), n3.getn()))
            
        main()
        1 + 2 = 3
        ```

- static 메소드보다 class 메소드가 더 어울리는 경우

    ```python
    class Date:  # 날짜를 표현한 클래스
        def __init__(self, y, m, d):
            self.y = y  # 년
            self.m = m  # 월
            self.d = d  # 일
        def show(self):
            print('{0}, {1}, {2}'.format(self.y, self.m, self.d))
        @classmethod
        def next_day(cls, today):  # today 다음 날에 대한 객체 생성 및 반환
            return cls(today.y, today.m, today.d + 1)
        
    def main():
        d1 = Date(2025, 4, 5)
        d1.show()
        d2 = Date.next_day(d1)
        d2.show()
        
    main()
    2025, 4, 5
    2025, 4, 6
    ```

- static 메소드보다 class 메소드가 완전 더 어울리는 경우
    - class 메소드는 인자로 클래스 정보를 받는다. 그리고 이 정보는 호출 경로에 따라서 유동적이다.

    ```python
    class Date:  # 앞서 예제에서 보인 Date 클래스와 완전히 동일하다.
        def __init__(self, y, m, d):
            self.y = y
            self.m = m
            self.d = d
        def show(self):
            print('{0}, {1}, {2}'.format(self.y, self.m, self.d))
        @classmethod
        def next_day(cls, today):
            return cls(today.y, today.m, today.d + 1)
        
    class KDate(Date):  # Date 클래스 상속, 한국의 시각 출력
        def show(self):
            print('KOR: {0}, {1}, {2}'.format(self.y, self.m, self.d))

    class JDate(Date):  # Date 클래스 상속, 일본의 시각 출력
        def show(self):
            print('JPN: {0}, {1}, {2}'.format(self.y, self.m, self.d))

    def main():
        kd1 = KDate(2025, 4, 12)  # 한국의 시각 정보
        kd1.show()
        kd2 = KDate.next_day(kd1)  # 다음 날 정보 생성, KDate 객체 생성 및 반환
        kd2.show()  # KDate 객체이므로 KOR로 출력 시작
        
        jd1 = JDate(2027, 5, 19)  # 일본의 시각 정보
        jd1.show()
        jd2 = JDate.next_day(jd1)  # 다음 날 정보 생성, JDate 객체 생성 및 반환
        jd2.show()  # JDate 객체이므로 JPN로 출력 시작
        
    main()
    KOR: 2025, 4, 12
    KOR: 2025, 4, 13
    JPN: 2027, 5, 19
    JPN: 2027, 5, 20
    ```