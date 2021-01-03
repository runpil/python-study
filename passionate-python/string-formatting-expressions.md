## 표현식 기반 문자열 조합 (String formatting expressions)
- '__%s_%s__' % (values, value) 스타일 문자열 조합

    ```python

    # 일반적인 문자열 조합
    friends = [('Jung', 22), ('Hong', 23), ('Part', 24)]  # 이름과 나이를 담은 리스트
    for f in friends:
        print('My friend', f[0], 'is', f[1], 'years old.')  # 출력할 내용을 각각 전달
    My friend Jung is 22 years old.
    My friend Hong is 23 years old.
    My friend Part is 24 years old.

    friends = [('Jung', 22), ('Hong', 23), ('Part', 24)]
    for f in friends:
        s = 'My friend ' + f[0] + ' is ' + str(f[1]) + ' years old.'
        print(s)
        # 위의 두 문장을 다음 하나로 대체할 수 있음, 그리고 이것이 더 일반적임
        #print('My friend ' + f[0] + ' is ' + str(f[1]) + ' years old.')
    My friend Jung is 22 years old.
    My friend Hong is 23 years old.
    My friend Part is 24 years old.

    # 표현식 기반으로 문자열 조합
    # %s : 이 위치에대가 문자열을 넣어라.
    # %d : 이 위치에다가 정수를 넣어라. (10진수 형태의 정수)
    # %f : 이 위치에다가 실수를 넣어라.
    s = 'My name is %s' % 'Yoon'  # %s 위치에 문자열 'Yoon'이 삽입됨
    s
    'My name is Yoon'

    friends = [('Jung', 22), ('Hong', 23), ('Part', 24)]
    for f in friends:
        print('My friend %s is %d years old' % (f[0], f[1]))
    My friend Jung is 22 years old
    My friend Hong is 23 years old
    My friend Part is 24 years old
    ```

- 자동 형변환

    ```python
    print('%d' % '둘')  # %d가 등장했으니 %의 오른쪽에 정수가 와야 한다.
    ---------------------------------------------------------------------------
    TypeError                                 Traceback (most recent call last)
    <ipython-input-18-b8f2c56843aa> in <module>
    ----> 1 print('%d' % '둘')  # %d가 등장했으니 %의 오른쪽에 정수가 와야 한다.

    TypeError: %d format: a number is required, not str

    # %s가 등장하면 문자열 이외에 원하는 것 대부분을 가져다 놓을 수 있다.
    # 이것이 가능한 이유는 파이썬이 형 변환을 해주기 때문이다.
    # 정수 22를 문자열 '22'로 바꿔준다.
    s = 'My friend %s is %s years old and %scm tall.' % ('Jung', 22, 178.5)
    s
    'My friend Jung is 22 years old and 178.5cm tall.'

    # 자동 변환이 발생하는 상황
    #   - 정수를 %f의 위치에 가져다 놓는 경우, 정수가 실수로 자동 변환된다.
    #   - 실수를 %d의 위치에 가져다 놓는 경우, 실수가 정수로 자동 변환된다. (소수점 이하 값 사라짐, 데이터 손실 발생)
    print('%f' % 25)
    25.000000
    print('%d' % 3.14)
    3
    ```

- 튜플 말고 딕셔너리로 출력 대상 지정하기

    ```python
    s = "%(name)s: %(age)d" % {'name': 'Yoon', 'age': 22}
    s
    'Yoon: 22'
    ```

- 보다 세밀한 문자열 조합 지정
    - %[flags][width][.precision]f
        - [flags] : - 또는 0 또는 +를 넣어서 특별한 신호를 줌
            - + : 부호 정보도 함께 출력을 해라. (0보다 크면 +, 작으면 -를 붙여서 출력해라.)
            - 0 : 빈 공간을 0으로 채워라
            - - : 공간이 남을 때는 왼쪽으로 붙여서 출력을 해라.
        - [width] : 폭, 어느 정도 넓이를 확보하고 출력할지 결정
        - [.precision] : 정밀도, 소수 이하 몇째 자리까지 출력할지 결정

    ```python
    'height: %f' % 3.14  # 정밀도 설정 없이 출력
    'height: 3.140000'

    'height: %.3f' % 3.14  # 소수점 이하 셋째 자리까지 출력
    'height: 3.140'

    'height: %.2f' % 3.14  # 소수점 이하 둘째 자리까지 출력
    'height: 3.14'

    'height: %7.2f입니다' % 3.14  # 7칸 확보하고 그 공간에 3.14를 넣음
    'height:    3.14입니다'

    'height: %10.2f입니다' % 3.14  # 10칸 확보하고 그 공간에 3.14를 넣음
    'height:       3.14입니다'

    'height: %07.2f입니다' % 3.14  # 7칸 확보하고 빈 공간을 0으로 채움
    'height: 0003.14입니다'

    'height: %010.2f입니다' % 3.14  # 10칸 확보하고 빈 공간을 0으로 채움
    'height: 0000003.14입니다'

    'height: %-7.2f입니다' % 3.14  # -는 왼쪽으로 붙여서 출력을 의미한다.
    'height: 3.14   입니다'

    'height: %-10.2f입니다' % 3.14  # -는 왼쪽으로 붙여서 출력을 의미한다.
    'height: 3.14      입니다'

    n = 3
    'num: %+d' % n  # [flags]에 +를 두면 부호가 함께 출력
    'num: +3'

    n = -1
    'num: %+d' % n  # [flags]에 +를 두면 부호가 함께 출력
    'num: -1'
    ```