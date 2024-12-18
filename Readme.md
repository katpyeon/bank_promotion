# 불균형 데이터 처리 with Orange3
불균형 데이터를 오렌지3에서 처리하는 방법을 정리한 레포지토리입니다.


### 개발 환경
- Mac OS Apple Silicon

### 오렌지 설치 
```
brew install orange
```

### imbalanced-learn 라이브러리 설치
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


# 처리 아디이어
- Over Sampling으로 소수데이터를 늘림
- Over Sampling된 데이터로 학습하고 학습되지 않은 데이터로 평가
- 피쳐 엔지니어링 하지 않음. 모델만으로 처리
- Recall 최대화
- 
# 변수 설명 (은행 정기예금 프로모션 데이터)

| 변수명        | 설명                                                                                       | 데이터 유형  | 예제 값       |
|---------------|--------------------------------------------------------------------------------------------|--------------|---------------|
| **ID**        | 각 고객의 고유 식별자                                                                      | `object`     | `train00001`  |
| **age**       | 고객의 나이                                                                                | `int64`      | `34`          |
| **job**       | 고객의 직업 (예: blue-collar, management 등)                                                | `object`     | `blue-collar` |
| **marital**   | 고객의 결혼 상태 (예: married, single, divorced)                                            | `object`     | `married`     |
| **education** | 고객의 교육 수준 (예: primary, secondary, tertiary 등)                                      | `object`     | `secondary`   |
| **default**   | 신용 불량 여부 (예: yes, no)                                                               | `object`     | `no`          |
| **balance**   | 고객의 은행 계좌 잔고                                                                      | `int64`      | `358`         |
| **housing**   | 주택 대출 여부 (예: yes, no)                                                               | `object`     | `yes`         |
| **loan**      | 개인 대출 여부 (예: yes, no)                                                               | `object`     | `no`          |
| **contact**   | 마지막으로 연락한 방식 (예: cellular, telephone, unknown)                                   | `object`     | `unknown`     |
| **day**       | 마지막으로 연락한 날 (달력 날짜, 1~31)                                                     | `int64`      | `23`          |
| **month**     | 마지막으로 연락한 월 (예: jan, feb, mar 등)                                                | `object`     | `may`         |
| **duration**  | 마지막으로 통화한 시간 (초 단위)                                                           | `int64`      | `100`         |
| **campaign**  | 현재 캠페인 동안 고객에게 연락한 횟수                                                      | `int64`      | `4`           |
| **pdays**     | 이전 캠페인 이후 연락까지 걸린 일수 (-1이면 이전 캠페인에서 연락받은 적 없음)                | `int64`      | `-1`          |
| **previous**  | 이전 캠페인 동안 고객에게 연락한 횟수                                                      | `int64`      | `0`           |
| **poutcome**  | 이전 캠페인의 결과 (예: success, failure, unknown 등)                                       | `object`     | `unknown`     |
| **label**     | **정기예금 신청 여부** (0: 신청하지 않음, 1: 신청함) **[목적 변수]**                        | `int64`      | `0`           |

## 목적 변수
- **`label`**: 정기예금 프로모션의 성공 여부를 나타내는 **이진 분류 문제**의 타겟 변수입니다.
  - `0`: 고객이 정기예금을 신청하지 않음
  - `1`: 고객이 정기예금을 신청함