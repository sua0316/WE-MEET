# 한파 예측 및 시각화 (WE-MEET 프로젝트)

기상 데이터를 기반으로 지역별 한파특보(주의보/경보) 발효 여부를 예측하고, 시각화를 통해 주요 위험지역과 시기적 경향성을 분석하는 프로젝트입니다. KNN 및 Random Forest 모델을 활용한 머신러닝 예측과 Elastic Stack 기반 시각화를 통해 한파 피해를 사전에 대비할 수 있는 정보를 제공합니다.


## 프로젝트 개요

- **프로젝트명**: WE-MEET - 날씨(한파) 예측 및 시각화
- **기간**: 2023.01.13 ~ 2023.01.27
- **데이터 출처**: 기상청 날씨이슈별 데이터(한파)  
  [기상자료개방포털](https://data.kma.go.kr/data/weatherIssue/cdwvList.do?pgmNo=723)
- **분석 범위**: 2020.11 ~ 2023.01 (매년 11월 ~ 4월)
- **사용 도구**: Python, scikit-learn, pandas, Elasticsearch, Kibana


## 프로젝트 목적

- 지역별 한파 여부를 사전 예측해 **동상, 저체온증 등 질병 예방**
- 시각화된 통계를 통해 **시설물 관리, 재난 대비** 기반 제공
- 실제 행정기관(서울시 상수도사업본부 등)에서 활용하는 **동파가능지수**를 예측에 반영


## 데이터 및 전처리 과정

- 총 68,526개의 행, 19개의 변수 → 결측치 제거 및 전처리 후 66,325행으로 축소
- 주요 전처리 내용:
  - 동파가능지수 및 기온, 풍속, 습도 등 결측치 처리
  - 스케일링 (StandardScaler), 범주형 변수 인코딩
  - 상관관계가 낮은 변수 제거


## 모델링

### KNN (K-Nearest Neighbors)
- **K-Fold 교차 검증** 평균 정확도: 0.9167
- **하이퍼파라미터 최적화** (`n_neighbors=20`) 결과
  - Train Accuracy: 0.929
  - Test Accuracy: 0.923
  - 1월 실제 예측 정확도: **0.92**

### Random Forest
- **Grid Search 최적화**: `n_estimators=600`, `max_features=sqrt`
- 중요 피처: `일평균기온`, `일최저기온`
  - Train Accuracy: 0.999
  - Test Accuracy: 0.921
  - 1월 실제 예측 정확도: **0.92**


## 데이터 시각화 (Elastic Stack)

- **월별 한파주의보 및 경보 빈도 분석**
- **한파 경보 발생 TOP10 지역** 도넛 차트 및 Word Cloud
- **한파 특보 발효 시 평균 최저 기온**
  - 미발효 시: 영상
  - 주의보 발효 시: 약 -9℃
  - 경보 발효 시: 약 -12℃
- **동파가능지수와 특보 발효 간 상관관계 분석**


## 기술 스택

- `Python`, `pandas`, `numpy`
- `scikit-learn`, `matplotlib`
- `Elasticsearch`, `Kibana`
- `StandardScaler`, `GridSearchCV`, `RandomSearchCV`


## 기대 효과

- 사용자 및 기관이 **지역별 한파 예측 정보를 기반으로 사전 대비** 가능
- **2020~2023년 한파 통계 시각화**를 통해 지역별 위험도 파악 용이
- 향후 `SMOTE`, `Undersampling` 등의 **Class imbalance 해결방안 적용 예정**
