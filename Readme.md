# 불균형 데이터 처리 with Orange3
불균형 데이터를 오렌지3에서 처리하는 방법을 정리한 레포지토리입니다.


### 개발 환경
- Mac OS Apple Silicon

### 오렌지 설치 
```
brew install orange
```

### imbalanced-learn 설치
- 오렌지가 설치된 환경에서 실행해야함. 파이썬 버전은 본인의 환경에 맞게 변경해야함.
- 터미널에서 아래 명령 실행시 보안 문제로 실행이 안될 수 있음. (맥에서 디스크 접근 불가 메세지 보여줌)
- 설정 -> 개인정보 보호 및 보안 -> 앱 관리 -> 터미널(iterm, wrap...) 스위치 O
- 다시 터미널에서 아래 명령 실행
    ```
    /Applications/Orange.app/Contents/Frameworks/Python.framework/Versions/3.11/bin/pip install --target=/Applications/Orange.app/Contents/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages imbalanced-learn
    ```
- 설치확인 방법
- 오렌지 재실행 > Python Script 추가 > 아래 코드 실행
- 에러 나오면 chatgpt 에게 물어보기
    ```
    import sys
    print(sys.path)
    import imblearn
    print("설치 완료:", imblearn.__version__)
    ```
