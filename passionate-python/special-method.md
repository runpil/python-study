## 스폐셜 메소드
- 다음과 같은 형태의 이름을 가지면서 파이썬에 의해 호출되는(프로그래머가 그 이름을 직접 명시하여 호출하지 않는) 메소드를 가리켜 '스폐셜 메소드(special methods)'라 한다.
    - ```__name__```
    - ```__init__``` :  객체 생성 시 자동으로 호출되는 메소드
    - ```__len__``` : len 함수가 호출되었을 때 호출됨
    - ```__iter__``` : iter 함수가 호출되었을 때 호출됨
    - ```__str__``` : str 함수가 호출되었을 때 호출됨

    ```python
    t = (1, 2, 3)
    len(t)  # t.__len__()
    3

    itr = iter(t)  # itr = t.__iter__()
    for i in itr:
        print(i, end = ' ')
    1 2 3

    s = str(t)  # s = t.__str__()
    s
    '(1, 2, 3)'
    ```

- 클래스에 스폐셜 메소드 정의하기

    ```python
    class Car:
        def __init__(self, id):
            self.id = id  # 차량 번호
        def __len__(self):
            return len(self.id)  # 차량 번호의 길이 반환됨
        def __str__(self):
            return 'Vehicle number : ' + self.id
        
    def main():
        c = Car("32러5234")
        print(len(c))  # __len__ 메소드 호출됨
        print(str(c))  # __str__ 메소드가 호출됨
        
    main()
    7
    Vehicle number : 32러5234
    ```

- iterable 객체가 되게끔 하기
    - iterable 객체 : iter 함수에 인자로 전달 가능한 객체, 그 결과로 'iterator 객체' 반환
    - iterator 객체 : next 함수에 인자로 전달 가능한 객체

    ```python
    class Car:
        def __init__(self, id):
            self.id = id
        def __iter__(self):  # 스폐셜 메소드
            return iter(self.id)  # 변수 id의 iterator 객체를 반환
        
    def main():
        c = Car("32러5234")
        for i in c:  # Car 객체가 iterable 객체라는 증거
            print(i, end = ' ')
            
    main()
    3 2 러 5 2 3 4
    ```

- iterator 객체가 되게끔 하기
    - iterator 객체가 되려면 다음 스폐셜 메소드를 갖고 있으면 된다.
        - ```__next__``` 메소드  : next 함수 호출 시 불리는 스폐셜 메소드
    - iterator 객체로 사용할 수 있는 수준으로 메소드가 정의되어야 한다.
        - 조건 1. 가지고 있는 값을 하나씩 반환한다.
        - 조건 2. 더 이상 반환할 값이 없는 경우 StopIteration 예외를 발생시킨다.

    ```python
    class Coll:  # 저장소 역할을 하는 클래스를 표현한 결과
        def __init__(self, d):
            self.ds = d  # 인자로 전달된 값을 저장한다.
            self.cc = 0  # __next__ 메소드 호출 횟수
        def __next__(self):
            if len(self.ds) <= self.cc:  # 더 이상 반환할 값이 없으면 예외 발생!
                raise StopIteration
            self.cc += 1  # __next__ 호출 횟수 증가
            return self.ds[self.cc - 1]  # 값을 하나씩 반환
        
    def main():
        co = Coll([1, 2, 3, 4, 5])  # 튜플 및 문자열도 전달할 수 있음
        while True:
            try:
                i = next(co)  # iterator 객체를 통해서 하나씩 꺼낸다.
                print(i, end = ' ')
            except StopIteration:  # 더 이상 꺼낼 값이 없으면,
                break  # 이 루프를 탈출한다.
                
    main()
    1 2 3 4 5
    ```

- iterator 객체이자 iterable 객체가 되게끔 하기
    - iterable 객체를 인자로 전달하면서 iter 함수를 호출하면 iterator 객체가 반환된다.

    ```python
    class Coll2:  
        def __init__(self, d):
            self.ds = d 
        def __next__(self):
            if len(self.ds) <= self.cc:  
                raise StopIteration
            self.cc += 1
            return self.ds[self.cc - 1]
        def __iter__(self):  # 이 메소드의 정의가 핵심!
            self.cc = 0  # next 호출 횟수 초기화
            return self  # 이 객체를 그대로 반환함
            
    def main():
        co = Coll2([1, 2, 3, 4, 5])
        for i in co:  # for 루프 진행 과정에서 iter 함수 호출됨
            print(i, end = ' ')
        for i in co:  # for 루프 진행 과정에서 iter 함수 호출됨
            print(i, end = ' ')
            
    main()
    1 2 3 4 5 1 2 3 4 5
    ```