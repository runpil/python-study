## dict & OrderedDict
- dict은 저장 순서를 유지하기 시작했다. (버전 3.7부터 유지하기 시작했다.)
- dict와 OrderedDict는 저장 순서를 정보로 보느냐 마느냐에 따른 차이

    ```python
    from collections import OrderedDict  # collections 모듈의 OrderedDict
    od = OrderedDict()  # OrderedDict 객체 생성
    od['a'] = 1  # 딕셔너리 사용 방법과 동일
    od['b'] = 2
    od['c'] = 3

    od
    OrderedDict([('a', 1), ('b', 2), ('c', 3)])

    for kv in od.items():  # 딕셔너리와 마찬가지로 items 메소드 호출 가능
        print(kv)

    ('a', 1)
    ('b', 2)
    ('c', 3)
    ```
- OrderedDict을 써야 할 이유가 있다면?

    ```python
    # dict
    d1 = dict(a = 1, b = 2, c = 3)
    d2 = dict(c = 3, a = 1, b = 2)

    d1
    {'a': 1, 'b': 2, 'c': 3}
    d2
    {'c': 3, 'a': 1, 'b': 2}

    d1 == d2  # d1, d2는 저장 순서가 다르고 내용물은 같다.
    True

    # OrderedDict
    from collections import OrderedDict
    od1 = OrderedDict(a = 1, b = 2, c = 3)  # dict 객체의 생성 방법과 동일
    od2 = OrderedDict(c = 3, a = 1, b = 2)

    od1
    OrderedDict([('a', 1), ('b', 2), ('c', 3)])
    od2
    OrderedDict([('c', 3), ('a', 1), ('b', 2)])

    od1 == od2
    False
    ```

- OrderedDict 저장 순서 이동

    ```python
    from collections import OrderedDict
    od = OrderedDict(a = 1, b = 2, c = 3)
    for kv in od.items():
        print(kv, end = ' ')

    ('a', 1) ('b', 2) ('c', 3)

    od.move_to_end('b')  # 키가 'b'인 키와 값을 맨 뒤로 이동
    for kv in od.items():
        print(kv, end = ' ')

    ('a', 1) ('c', 3) ('b', 2)

    od.move_to_end('b', last = False)  # 매개변수 last에 False를 전달하면 맨 앞으로 이동
    for kv in od.items():
        print(kv, end = ' ')

    ('b', 2) ('a', 1) ('c', 3)
    ```

- 따라서 저장 순서 자체가 하나의 정보로써 의미를 갖는다면, 그리고 저장 순서를 바꿔야 할 가능성도 존재한다면, OrderedDict를 선택해야 한다.