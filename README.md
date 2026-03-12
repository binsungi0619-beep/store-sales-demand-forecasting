# 매장 운영 의사결정을 위한 수요 예측 및 프로모션 최적 시점 제안

## 프로젝트 정보

**기간**  
2025.12 (4주)

**팀 구성**  
5인 팀 프로젝트

**역할**  
PM 및 수요 예측 모델링 전반 주도

---

# 1. 프로젝트 개요

Kaggle Store Sales 데이터(약 **1억 2,500만 건 / 5.39GB**)를 활용하여  
매장 운영 의사결정을 지원하는 **수요 예측 및 프로모션 전략 도출 프로젝트**입니다.

단순 판매량 예측 모델을 구축하는 것에서 나아가,

- 운영 안정화를 위한 **Base 수요 예측 모델**
- 마케팅 전략 도출을 위한 **Event 프로모션 효과 예측 모델**

을 **이원화 구조**로 설계하여 실제 매장 운영 전략에 활용 가능한 분석을 목표로 했습니다.

또한 매장 단위가 아닌 **수요 패턴 기반 클러스터 단위 분석**을 통해  
지역·클러스터별 차등 운영 전략을 도출했습니다.

---

# 2. 데이터

**Kaggle Store Sales Dataset**

- 약 **125M rows**
- 데이터 크기 **5.39GB**

### 사용 데이터

- Sales  
- Stores  
- Items  
- Transactions  
- Holidays & Events  
- Promotions  
- External Weather Data (Open-Meteo API)

---

# 3. 주요 문제 정의

본 프로젝트는 다음 질문에서 시작되었습니다.

> **"축제 기간 동안 언제 프로모션을 진행하는 것이 가장 효과적인가?"**

이를 해결하기 위해 다음 두 가지 분석을 수행했습니다.

### 1) Base Model
외부 이벤트가 없는 **기본 수요를 예측하여 운영 기준선 확보**

### 2) Event Model
축제 기간 **프로모션 효과(Uplift)를 분석하여 최적 프로모션 시점 제안**

---

# 4. 데이터 전처리 및 엔지니어링

대용량 데이터 처리 과정에서 다음과 같은 최적화를 수행했습니다.

### 메모리 최적화

- Data Full Load 전략 적용
- dtype 최적화 (float64 → float32 등)
- Parquet 기반 데이터 처리

**결과**

- 메모리 사용량 **41.2% 감소**
- **5.39GB → 3.16GB**
- 팀 전체 **커널 재시작 문제 해결**

---

# 5. 매장 클러스터링

매출 규모가 아닌 **수요 패턴 기반 매장 그룹화**를 수행했습니다.

### 방법

- Hierarchical Clustering  
- K-Means Clustering  
- Elbow Method  
- Silhouette Score  

### 결과

- 총 **8개 클러스터 도출**
- 지역별 수요 패턴 차이 확인

이를 기반으로 **클러스터 단위 운영 전략 수립이 가능하도록 설계했습니다.**

---

# 6. Base 판매량 예측 모델

운영 안정화를 위한 **기본 수요 예측 모델**을 구축했습니다.

### 특징

- 재귀 예측 구조 적용
- TimeSeries Cross Validation
- 데이터 누수 방지 설계

### 모델 비교

- CatBoost
- XGBoost
- LightGBM
- RandomForest

### 결과

클러스터 평균 성능

- **R² : 0.73**
- **RMSLE : 1.84**

---

# 7. Event 프로모션 효과 분석

축제 기간 동안의 **판매량 상승 효과(Uplift)** 를 예측했습니다.

### Uplift 정의

- (축제 판매량 - Baseline) / Baseline


### Baseline

- 축제 이전 **D-60 ~ D-4**
- 프로모션 없는 기간

### 모델

- CatBoost
- Optuna 하이퍼파라미터 튜닝

### 결과

- **Navidad 축제 Uplift +42.2%**
- **방향성 정확도 64.3%**

(랜덤 기준 33% 대비 약 2배)

---

# 8. 대시보드 구축

**Streamlit 기반 의사결정 지원 대시보드**를 구축했습니다.

### 대시보드 기능

- 매장 운영 KPI 모니터링
- 지역별 판매량 분석
- 수요 예측 결과 시각화
- 프로모션 효과 시뮬레이션

---

# 9. 기술 스택

### Language
- Python
- SQL

### Data Processing
- Pandas
- NumPy
- Parquet

### Modeling
- CatBoost
- XGBoost
- LightGBM
- Scikit-learn

### Data Engineering
- Airflow
- Snowflake

### Visualization
- Streamlit
- Plotly

---

# 10. 결과 및 인사이트

본 프로젝트를 통해

- **대용량 데이터 처리 최적화 경험**
- **실제 운영 환경을 고려한 시계열 예측 모델 설계**
- **데이터 기반 마케팅 전략 도출**

을 경험했습니다.

특히 **Base 모델과 Event 모델을 분리한 이원화 구조**를 통해  
운영 안정성과 전략적 의사결정을 동시에 지원하는 분석 구조를 설계했습니다.

---

# 11. Dashboard

Streamlit Dashboard (Snowflake 연동 환경)

※ 현재 Snowflake 데이터 연결 제한으로 인해  
**대시보드 실시간 실행은 제한되어 있습니다.**

대시보드 화면 및 기능은 아래 포트폴리오에서 확인할 수 있습니다.

---

# 12. 포트폴리오

전체 분석 과정 및 결과는 아래 포트폴리오에서 확인할 수 있습니다.

📄 **Portfolio PDF**  
(여기에 Google Drive 링크 삽입)
