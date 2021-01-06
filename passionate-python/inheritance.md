## 상속
- 부모 클래스, 슈퍼 클래스, 상위 클래스
자식 클래스, 서브 클래스, 하위 클래스
- 부모 클래수가 갖는 모드 메소드가 자식 클래스에도 담긴다.
- 자식 클래스에는 별도의 메소드를 추가할 수 있다.
- 상속 예시

    ```python
    class Father:
        def run(self):  # 달리기 능력이 있음
            print("so fast!!!")

    class Son(Father):  # Father 클래스를 상속하는 Son 클래스
        def jump(self):  # 점프 능력이 있음
            print("so high!!!")
            
    def main():
        s = Son()  # 아빠 객체를 생성해서 s에 담음
        s.run()  # 아빠에게 물려받은 run 메소드 호출
        s.jump()  # 별도로 추가한 jump 메소드 호출
        
    main()
    so fast!!!
    so high!!!
    ```

- 둘 이상의 클래스 상속

    ```python
    class Father:
        def run(self):  # 아빠는 달리기 능력이 있음
            print("so fast!!!")

    class Mother:
        def dive(self):  # 엄마는 잠수하는 능력이 있음
            print("so deep!!")
            
    class Son(Father, Mother):  # Father와 Mother를 동시 상속하는 Son 클래스
        def jump(self):  # 아들은 추가로 점프 능력을 갖고 태어남
            print("so high!!!")
            
    def main():
        s = Son()  # 아들 객체 생성
        s.run()  # 아빠로부터 물려받은 능력
        s.dive()  # 엄마로부터 물려받은 능력
        s.jump()  # 아들이 추가로 갖고 태어난 능력
        
    main()
    so fast!!!
    so deep!!
    so high!!!
    ```

- 메소드 오버라이딩과 super
    - 메소드 오버라이딩은 기능보강을 위해 필요

    ```python
    class Father:
        def run(self):
            print("so fast, dad style")

    class Son(Father):
        def run(self):  # Father 클래스의 run 메소드를 가림(오버라이딩 함)
            print("so fast, son style")
            
    def main():
        s = Son()
        s.run()  # Son의 run 메소드가 호출된다.
        
    main()
    so fast, son style

    # 부모 클래스에 오버라이딩 된 메소드 호출 방법
    class Father:
        def run(self):
            print("so fast, dad style")

    class Son(Father):
        def run(self):
            print("so fast, son style")
        def run2(self):
            super().run()  # 부모 클래스의 run 호출 방법, 가려진 run 호출 방법
            
    def main():
        s = Son()
        s.run()
        s.run2()
        
    main()
    so fast, son style
    so fast, dad style
    ```

- __init__ 메소드의 오버라이딩
    - 메소드 오버라이딩을 할 수밖에 없으면서 동시에 가려진 메소드(오버라이딩 된 메소드)를 호출해야하는 상황에 사용

    ```python
    class Car:
        def __init__(self, id, f):
            self.id = id  # 차량번호
            self.fuel = f  # 남아 있는 연료의 상태
        def drive(self):
            self.fuel -= 10
        def add_fuel(self, f):  # 연료 보충
            self.fuel += f
        def show_info(self):  # 현재 차의 상태 출력
            print("id:", self.id)
            print("feul:", self.fuel)
            
    class Truck(Car):
        def __init__(self, id, f, c):
            super().__init__(id, f)  # Car의 __init__ 메소드 호출
            self.cargo = c  # 차에 실려 있는 짐의 양
        def add_cargo(self, c):  # 짐을 추가한다.
            self.cargo += c
        def show_info(self):  # 현재 차의 상태 출력 (기능보강)
            super().show_info()  # Car의 show_info 메소드 호출
            print("cargo:", self.cargo)
            
    def main():
        t = Truck("42럭5959", 0, 0)
        t.add_fuel(100)
        t.add_cargo(50)
        t.drive()
        t.show_info()
        
    main()
    id: 42럭5959
    feul: 90
    cargo: 50
    ```