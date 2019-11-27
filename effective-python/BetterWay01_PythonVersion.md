# Better way 01 사용중인 파이썬의 버전을 알자

## 1. --version 플래그 이용
```
$ python --version
>>> Python 3.6.2 :: Anaconda, Inc.
```

## 2. sys 모듈 이용
```python
import sys
print(sys.version_info)
print(sys.version)

>>> sys.version_info(major=3, minor=6, micro=2, releaselevel='final', serial=0)
>>> 3.6.2 |Anaconda, Inc.| (default, Sep 19 2017, 08:03:39) [MSC v.1900 64 bit (AMD64)]
```

### 핵심정리
- 파이썬의 주요 버전인 파이썬 2, 파이썬 3 모두 여전히 활발히 사용된다.
- 파이썬에는 CPython, Jython, IronPython, PyPy 같은 다양한 런타임이 있다.
- 시스템에서 파이썬을 실행하는 명령이 사용하고자 하는 파이썬 버전인지 확인해야 한다.
- 파이썬 커뮤니티에서 주로 다루는 버전은 파이썬 3이므로 새 파이썬 프로젝트를 시작할 때는 파이썬 3를 사용하는 편이 좋다.