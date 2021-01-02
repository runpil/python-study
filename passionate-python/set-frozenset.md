## 자료형 분류와 set & frozenset
- 시퀀스 타입(sequence type)
    - 저장된 값의 순서 정보가 존재하는 것이 가장 큰 특징
    - 시퀀스 타입의 종류
        - 리스트 : list 클래스의 객체
        - 튜플 : tuple 클래스의 객체
        - 레인지 : range 클래스의 객체
        - 문자열 : str 클래스의 객체
    - 시퀀스 타입의 두 가지 연산
        - 인덱싱 연산 : 특정 값 하나를 참조하는 연산

            ex) s[0], s[1], s[2]

        - 슬라이싱 연산 : 시작과 끝을 정하여 이를 참조하는 연산

            ex) s[0:3], s[5:9]

- 매핑 타입(mapping type)
    - 본질적으로 저장된 값의 순서 또는 위치 정보를 기록하지 않는 자료형
    - 버전 3.7부터 저장된 값의 순서를 유지하기 시작했으나 그렇다고 해서 본질이 바뀌지 않는다.
    - 때문에 이를 대상으로는 인덱싱이나 슬라이싱 연산이 불가능하다.
    - 매핑 타입의 종류
        - 딕셔너리 : dict 클래스의 객체
- 셋 타입(set type)
    - 수학의 '집합'을 표현한 자료형
    - 셋 타입의 종류
        - 셋(set) : set 클래스의 객체
        - 프로즌셋 : frozenset 클래스의 객체
    - 특징
        - 수학의 집합은 저장 순서를 유지하지 않는다.
        - 수학의 집합은 중복된 값의 저장을 허용하지 않는다.
- set, frozenset
    - 두 집합을 대상으로 하는 수학의 기본 연산
        - 합집합 : 두 집합의 모든 원소들을 합친 집합
        - 차집합 : 한 집합에서 다른 한 집합이 갖는 원소들을 뺀 집합
        - 교집합 : 두 집합에서 공통으로 존재하는 원소들의 집합
        - 대칭 차집합 : 두 집합의 합집합에서 교집합을 뺀 집합
    - set 연산 예

        ```python
        # ex1
        A = {'a', 'c', 'd', 'f'}  # 집합 A, 이것이 셋을 생성하는 기본 방법
        B = {'a', 'b', 'd', 'e'}  # 집합 B

        A - B  # A에 대한 B의 차집합
        {'c', 'f'}
        A & B  # A와 B의 교집합
        {'a', 'd'}
        A | B  # A와 B의 합집합
        {'a', 'b', 'c', 'd', 'e', 'f'}
        A ^ B  # A와 B의 대칭 차집합
        {'b', 'c', 'e', 'f'}

        # ex2
        A = set(['a', 'c', 'd', 'f'])  # set 함수에 iterable 객체 전달해서 set 생성
        B = set('fdca')  # 문자열도 iterable 객체이므로 이를 통해 set 생성 가능

        A
        {'d', 'a', 'c', 'f'}
        B
        {'d', 'c', 'f', 'a'}
        A == B  # 저장 순서는 상관없다. 내용물만 같으면 True
        True
        'a' in A  # 집합 A에 원소 'a'가 있는가?
        True
        'b' not in A  # 집합 A에 원소 'b'가 없는가?
        Ture
        for c in A & B:  # A & B의 결과로 얻은 집합을 대상으로 for 루프 구성
            print(c, end = ' ')
        d a c f

        # 빈 set 생성
        s = set()  # 빈 set을 생성하는 방법
        type(s)
        <class 'set'>
        ```

    - frozenset 예

        ```python
        A = frozenset(['a', 'c', 'd', 'f'])  # frozenset 함수에 iterable 객체 전달해서 생성
        B = frozenset(['a', 'b', 'd', 'e'])

        A - B
        frozenset({'c', 'f'})
        A | B
        frozenset({'a', 'b', 'c', 'd', 'e', 'f'})
        A == B
        False
        'a' in A
        True
        for c in A & B:
            print(c, end = ' ')
        d a
        ```

    - set을 이용한 중복된 값 삭제
        - 중복을 허용하지 않는 set의 특성 활용

        ```python
        t = [3, 3, 3, 7, 7, 'z', 'z']
        t = list(set(t))  # t를 가지고 set을 구성하고, 다시 그 결과로 리스트 구성!

        t
        ['z', 3, 7]
        ```

    - set, frozenset 차이점
        - set : mutable 객체
        - frozenset : immutable 객체
        - 즉 set은 새로운 값의 추가 또는 삭제가 가능한 반면 frozenset은 불가능하다.
        - 기존에 존재하던 객체의 값을 수정하는 연산은 set을 대상으로만 할 수 있다. (set이 추가로 가지고 있는 연산)
            - add : 원소 추가하기
            - discard : 원소 삭제하기
            - update, |= : 다른 집합의 원소 전부 추가하기
            - intersection_update, &= : 다른 집합과 공통으로 있는 원소만 남기기
            - difference_update, -= : 다른 집합이 갖는 원소 모두 삭제하기
            - symmetric_difference_update, ^= : 공통으로 갖지 않는 것들은 추가하고 나머지는 삭제
        - 예

            ```python
            os = {1, 2, 3, 4, 5}  # 이 변수에 담긴 set을 이제부터 수정한다.

            os.add(6)  # 원소 6을 집합 os에 추가
            os.discard(1)  # 원소 1을 집합 os에서 삭제
            os
            {2, 3, 4, 5, 6}
            os.update({7, 8, 9})  # 집합 os에 {7, 8, 9}의 모든 원소 추가
            os
            {2, 3, 4, 5, 6, 7, 8, 9}
            os &= {2, 4, 6, 8}  # 집합 os에서 {2, 4, 6, 8}와 겹치는 원소만 남김
            os
            {2, 4, 6, 8}
            os -= {2, 4}  # 집합 os에서 {2, 4}의 원소를 모두 삭제
            os
            {6, 8}
            os ^= {1, 3, 6}  # 집합 os에서 {1, 3, 6}에 있는 원소는 빼고 없는 원소는 추가
            os
            {1, 3, 8}
            ```

        - set 컴프리헨션

            ```python
            s1 = {x for x in range(1, 11)}
            s1
            {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

            s2 = {x**2 for x in s1}
            s2
            {1, 4, 9, 16, 25, 36, 49, 64, 81, 100}

            s3 = {x for x in s2 if x < 50}
            s3
            {1, 4, 9, 16, 25, 36, 49}
            ```