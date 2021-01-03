## 파이썬 정렬 기술
- 리스트의 sort 메소드
    - 리스트 자체를 수정

    ```python
    # 오름차순 정렬
    ns = [3, 1, 4, 2]
    ns.sort()
    ns
    [1, 2, 3, 4]

    # 내림차순 정렬
    ns = [3, 1, 4, 2]
    ns.sort(reverse = True)
    ns
    [4, 3, 2, 1]

    # key 매개변수를 이용한 정렬 (특정 데이터 기준으로 정렬할 때 사용)
    # 리스트에 저장된 튜플 정렬 (나이 기준 정렬)
    ns = [('Yoon', 33), ('Lee', 12), ('Park', 29)]
    def age(t):
        return t[1]  # 나이 반환하는 함수

    ns.sort(key = age)  # 매개변수 key에 함수 age를 전달!
    ns
    [('Lee', 12), ('Park', 29), ('Yoon', 33)]

    ns.sort(key = age, reverse = True)  # 내림차순 정렬
    ns
    [('Yoon', 33), ('Park', 29), ('Lee', 12)]

    # 람다식으로 작성
    ns = [('Yoon', 33), ('Lee', 12), ('Part', 29)]
    ns.sort(key = lambda t : t[1], reverse = True)  # 이름의 알파벳 역순으로 정렬
    ns
    [('Yoon', 33), ('Part', 29), ('Lee', 12)]

    # 두 수의 합 정렬
    nums = [(3, 1), (2, 9), (0, 5)]
    nums.sort(key = lambda t : t[0] + t[1], reverse = True)
    nums
    [(2, 9), (0, 5), (3, 1)]
    ```

- sorted 함수
    - 원본은 그대로 두로 정렬된 사본이 필요한 경우 사용
    - 정렬된 사본을 새로 생성하기 때문에 iterable 객체면 무엇이든 전달 가능
    - 튜플은 내용을 수정할 수 없기 때문에 sort 메소드가 존재하지 않는다.
    - 정렬 결과는 리스트에 담아서 반환 된다.

    ```python
    org = [('Yoon', 33), ('Lee', 12), ('Part', 29)]  # (이름, 나이)
    cpy = sorted(org, key = lambda t : t[1], reverse = True)  # 나이 기준 내림차순 정렬
    org  # 원본이 유지된다.
    [('Yoon', 33), ('Lee', 12), ('Part', 29)]
    cpy  # 정렬된 사본이 생성되었다.
    [('Yoon', 33), ('Part', 29), ('Lee', 12)]

    # 정렬 결과는 리스트에 담긴다.
    org = (3, 1, 2)
    cpy = sorted(org)
    org
    (3, 1, 2)
    cpy
    [1, 2, 3]
    ```