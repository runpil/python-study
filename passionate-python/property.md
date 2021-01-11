## 프로퍼티
- 안전하게 접근하기
    - 객체가 갖는 값에 직접 접근하는 것은 오류의 확률을 높이므로 메소드를 통해 접근하는 것이 안전하다.

    ```python
    class Natural:  # 자연수 표현한 클래스, 따라서 이 객체에는 1 이상만 저장되어야 함
        def __init__(self, n):
            if(n < 1):  # 1 미만의 값이 들어오면,
                self.__n = 1  # 1을 기본 값으로 저장
            else:
                self.__n = n
        def getn(self):  # 저장된 값 꺼내기
            return self.__n
        def setn(self, n):  # 저장된 값 수정하기
            if(n < 1):  # 1 미만의 값이 들어오면,
                self.__n = 1  # 1을 기본값으로 저장
            else:
                self.__n = n
                
    def main():
        n = Natural(-3)  # 이 경우 -3 대신 1이 저장된다.
        print(n.getn())
        n.setn(2)
        print(n.getn())
        
    main()
    1
    2

    # 중복된 코드 제거
    class Natural:
        def __init__(self, n):
            self.setn(n)  # 아래에 있는 setn 메소드 호출로 중복된 코드를 대신했다.
        def getn(self):
            return self.__n
        def setn(self, n): 
            if(n < 1):  
                self.__n = 1 
            else:
                self.__n = n
                
    def main():
        n1 = Natural(1)
        n2 = Natural(2)
        n3 = Natural(3)
        n1.setn(n2.getn() + n3.getn())  # 조금 복잡해 보인다.
        print(n1.getn())
        
    main()
    5

    # 프로퍼티 설정
    class Natural:
        def __init__(self, n):
            self.setn(n)  # 아래에 있는 setn 메소드 호출
        def getn(self):
            return self.__n
        def setn(self, n): 
            if(n < 1):  
                self.__n = 1 
            else:
                self.__n = n
        n = property(getn, setn)  # 프로퍼티 설정
        
    def main():
        n1 = Natural(1)
        n2 = Natural(2)
        n3 = Natural(3)
        n1.n = n2.n + n3.n  # 간결해진 문장
        print(n1.n)  # 이 문장도 이전에 비해 간결해짐
        
    main()
    5
    ```