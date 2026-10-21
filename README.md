# 파인 스크립트 시그널 데이터 피드 (pine-signals)

TradingView Pine Script 및 자동매매 시스템(EA, Expert Advisor)을 위한 시그널·가격 데이터 저장소 및 자동 피드 레포지토리입니다.

지수 및 선물 종목(US100 등)의 실시간 시그널 상태와 OHLCV 데이터를 CSV 포맷으로 안전하게 기록·보관하며, 트레이딩 봇 및 외부 분석 도구와의 데이터 연동을 지원합니다.

---

## ⚡ 3초 요약 (가장 빠른 사용법)

1. **최신 시그널 데이터 즉시 확인**:  
   브라우저에서 **`data/US100.csv`**를 열거나 아래 cURL 명령어로 실시간 데이터를 조회합니다:
   ```bash
   curl -s https://raw.githubusercontent.com/juhyuck616-cmyk/pine-signals/main/data/US100.csv
   ```

2. **데이터 레코드 형식**:  
   표준 시계열 타임스탬프와 OHLCV 컬럼으로 구성됩니다:
   ```csv
   time,open,high,low,close,volume
   20260314T020304Z,-1,-1,-1,-1,0
   ```

---

## 🌟 주요 기능

* **실시간 트레이딩 시그널 아카이빙**:
  * 자동화 봇 및 웹훅(Webhook)에서 발생한 매매 신호를 GitHub 커밋으로 실시간 기록
  * US100(나스닥 100 지수) 등 핵심 감시 자산의 시그널 발생 상태 추적
* **경량화된 시계열 데이터 포맷 (CSV)**:
  * 별도의 무거운 데이터베이스 없이 표준 CSV 파일로 초경량 시그널 피드 제공
  * Pine Script, Python, Bash, Excel 등 다양한 환경에서 간편하게 연동 및 파싱 가능
* **Git 기반 무결성 보장 및 감사 로그**:
  * Git 커밋 타임스탬프와 커밋 메시지(`signal update: US100 (YYYY-MM-DD HH:mm)`)를 통한 발생 시점 영구 보존
  * 사후 전략 백테스팅 대조 및 신호 지연(Latency) 분석 지원

---

## 📁 파일 및 폴더 안내

| 파일 / 폴더 | 설명 |
| :--- | :--- |
| **`data/`** | 종목별 시그널 데이터 CSV 파일 보관 디렉터리 |
| **`data/US100.csv`** | US100(나스닥 100) 지수 시그널 및 가격 시계열 데이터 파일 |
| **`repo.json`** | 저장소 메타데이터 및 소유자 식별 설정 파일 |

---

## 💻 상세 사용법

### 1. Python에서 시그널 데이터 수신
```python
import pandas as pd

url = "https://raw.githubusercontent.com/juhyuck616-cmyk/pine-signals/main/data/US100.csv"
df = pd.read_csv(url)
print(df.tail())
```

### 2. cURL 및 Bash 환경에서 최신 값 확인
```bash
curl -s https://raw.githubusercontent.com/juhyuck616-cmyk/pine-signals/main/data/US100.csv | tail -n 1
```

### 3. 신규 종목 피드 확장 방법
1. `data/{심볼코드}.csv` 파일을 생성하고 헤더를 지정합니다:
   ```csv
   time,open,high,low,close,volume
   ```
2. 시그널 발생 시 새로운 데이터 행을 추가하고 커밋합니다:
   ```bash
   git commit -m "signal update: {심볼코드} (YYYY-MM-DD HH:mm)"
   ```

---

## 🔗 연동 및 참고 문서
- TradingView Pine Script 가이드: https://www.tradingview.com/pine-script-docs/
