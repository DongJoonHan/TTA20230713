# TTA20230713

# OpenJDK 설치
https://github.com/ojdkbuild/ojdkbuild

## 예제 프로젝트
- JS: https://github.com/bigskysoftware/htmx
- Py: https://github.com/geekan/MetaGPT

- Jenkins_Py: https://github.com/tinygrad/tinygrad
- Jenkins_PyJS: https://github.com/ladjs/superagent



# 룰 기반
  - Java: PMD
  - C/C++: CPPCheck
  - Python: Pylint
# 순환복잡도 / 함수 라인수
  - Lizard (Python 패키지)
# 중복코드
  - CPD (PMD의 부속 도구 / 언어 안가림)
    . 기준: Token/Chunk 100
# 전체 라인수/주석비율
  - CLOC


# 기타 참고자료
## Jenkins 에서 커버리지 표현하기
### 플러그인 설치
- Cobertura 플러그인 설치

## Unittest 결과를 Jenkins에서 보기
### Unitetest 결과의 xml 저장 도구 설치
pip install unittest-xml-reporting

### 실행
```
del testReport /s /f /q
python -m xmlrunner discover -o testReport
```

### Jenkins
Junit 테스트 결과와 매핑
![image](https://user-images.githubusercontent.com/8405564/155468303-37c4951d-b48e-4832-a899-0acaabe87460.png)

![image](https://user-images.githubusercontent.com/8405564/155468454-a899cd37-9b07-4dbe-ac50-4964e9331ecb.png)

```
testReport/TEST-*.xml
```


## Liazrd 설치 (순환복잡도 분석)
- 사전 조건: Python 설치

```
pip install lizard
```

### Lizard 실행해서 엑셀파일로 저장 (순환복잡도 10 이상)
```
lizard.exe -C 10 --csv > lizard_result.csv
```

### Jenkins를 위한 실행
```
lizard -C 10 -L 80 --xml > lizard.xml
```

### Jenkins 플러그인
CppNCSS 플러그인 이용

### Jenkins 설정
![image](https://user-images.githubusercontent.com/8405564/155474775-10bacab5-6bc3-43ee-9d11-49e2cd7a75e9.png)


## CPD 실행
100 Token 이상, C++ 을 대상으로 분석, 엑셀에서 확인하기 위해 csv로 출력해서 저장
```
cpd.bat --minimum-tokens 100 --files . --language py --format csv > cpd_result.csv
```

### Jenkins를 위한 실행
```
cpd --minimum-tokens 100 --files . --language py --format xml > cpd.xml
```

### Jenkins를 위한 설정
- Warning Next Generation 플러그인 이용
- 내부에서 CPD 지정


## CPPChcek 실행
```
"c:\Program Files\Cppcheck\cppcheck.exe" --enable=all --inconclusive --xml --xml-version=2 src 2> cppcheck.xml
```
