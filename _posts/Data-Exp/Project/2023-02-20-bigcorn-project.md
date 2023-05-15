---
title:  "2020 빅콘테스트 데이터분석 KBO 퓨처스리그 승률 예측 프로젝트" 
excerpt: "시계열 분석을 이용한 팀별 승률, 타율 및 방어율 예측 (with ARIMA)"

categories:
  - Project
tags:
  - [Analysis, Project]

toc: true
toc_sticky: true
 
date: 2023-02-20
last_modified_at: 2023-02-20

---

## 2020 KBO 퓨처스리그 예측 모델 개발 
### 시계열 분석을 이용한 팀별 승률, 타율 및 방어율 예측 (with ARIMA)

2020 빅콘테스트 데이터분석분야 KBO 퓨처스리그 NOVUS팀 분석 프로젝트입니다.   
2020.09 ~ 2020.10, 약 2달간 프로젝트를 진행했습니다. 

[프로젝트 코드 보관소](https://github.com/heoni00/2020-Project-Bigcon)

#### 참가 팀원 

구경민, 고건우, 김차헌

- 산업공학, 통계학, 정치외교학 학부 출신 
- 프로그래밍 언어, 회귀분석, 시계열에 관심 및 일정 수준의 이해에 기반하여 분석 진행
- 데이터 분석 및 AI 동아리를 구성하여 학습 및 프로젝트 경험을 위해 출전 

### OVERVIEW

![슬라이드1](https://user-images.githubusercontent.com/67791317/198822417-9a81e54d-ca8c-4371-8e91-03ff497fa6ee.jpeg)

#### 분석 주안점

- 객관적인 분석 (각 구단들의 축적된 정형 데이터만을 활용)
- 구단 속성의 변화 (스토브리그와 구단 환경 변화로 발생한 데이터 활용)
- 시계열 데이터 (매해 발생한 시계열 데이터 수집 및 ARIMA 모델 활용)

#### 분석 프로세스 요약 

![슬라이드7](https://user-images.githubusercontent.com/67791317/198822679-57433d21-4109-4820-a258-191c835a317f.jpeg)
![슬라이드8](https://user-images.githubusercontent.com/67791317/198822683-576197a2-3bfb-4eeb-99c0-214c29e87ef0.jpeg)

#### 데이터 전처리

1. 이상치 / 결측값 파악

- 시즌 및 시트별 투수[ER(자책점), WLS(승률) 칼럼]과 타자[HIT(안타수), AB(타수) 칼럼] 추출
- is.null & boxplot을 이용하여 결측치 및 이상치를 확인

2. 변수간의 관계 파악 / 파생변수 생성

- 승률 = WLS 칼럼 추출 후 팀별 그룹화, 문자열형을 숫자열형으로 치환 이후 이동평균을 구함
- 타율 = AB, HIT 칼럼 추출 후 팁별 그룹화, (AB / HIT)로 계산하여 타율 변수 생성 이후 이동평균 구함
- 평균 자책점 = ER 칼럼 추출 후 팀별 그룹화 이후 이동평균 구함

#### 모델링

1. ARIMA 모델

![슬라이드17](https://user-images.githubusercontent.com/67791317/198837217-204b33b3-4ed0-4088-8db9-3f318c524798.jpeg)

2. 모델 적용

- R tseries 패키지 auto.arima 이용하여 ARIMA 차수 산출
- ARIMA 차수 (0,1,0)가 나온다면 정상성을 유지하기 위해 모델을 조정하여 가장 aic값이 작은 차수를 구하여 재적용

![image](https://user-images.githubusercontent.com/67791317/198844406-9ca80eb6-15ae-4ac2-9d08-3bcce27d3df3.png)

- 산출된 ARIMA 차수를 python ARIMA 모델에 투입하여 최종 예측값 출력 및 시각화

![image](https://user-images.githubusercontent.com/67791317/198837716-4185b10c-ef9f-4e32-b58d-fdcf7b2760ae.jpeg)

3. 모델 검증 

- 모델로 출력한 예측값과 검증 데이터와 비교했을 때 예측 결과가 실제값과 다르다는 것을 인지

<img width="426" alt="image" src="https://user-images.githubusercontent.com/67791317/198837783-40c5010b-5e72-485f-a5a4-7a5a08044edc.png">

4. 모델 보완

- 적은 데이터의 한계를 해결하기 위해 20 시즌 추가 데이터를 추가. 
- 기존 ARIMA 차수의 비정상성을 제거하기 위한 차분 작업 세밀화

<img width="314" alt="image" src="https://user-images.githubusercontent.com/67791317/198837875-51ee8fa2-6ea9-4a2c-9c68-e23ad4080f50.png">

5. 분석 결과 

- [전체 분석 결과](https://github.com/heoni00/2020-Project-Bigcon/tree/main/Presentation#%EC%B5%9C%EC%A2%85-%EC%98%88%EC%B8%A1-%EA%B2%B0%EA%B3%BC)
- 예시

![슬라이드22](https://user-images.githubusercontent.com/67791317/198838000-5c7b939f-8f77-46c9-8f1a-c626848cc9bb.jpeg)

6. 사후 평가 

![슬라이드23](https://user-images.githubusercontent.com/67791317/198838035-3606e3a2-a32d-4655-a99d-7803e84480fd.jpeg)

#### 사용 언어 및 라이브러리/모듈

**R**
dplyr: 전처리를 위해 사용함. 
pracma: 수치데이터 전처리를 위해 사용함. 
forecast: 시계열 데이터 예측을 하기 위해 사용함.  
TTR: 시계열 데이터 분석을 위해 사용함.  
Tseries: 시계열 데이터 분석을 위해 사용함.  
  
**Python**
pandas: 데이터 프레임을 인식하고 전처리를 위해 사용함.  
numpy: 누락값을 읽기 위해 사용함.  
statsmodels: ARIMA모델을 사용하기 위해 사용함.  
matplot: 시각화를 위해 사용함.  

#### 레퍼런스

- “자기회귀이동평균(ARIMA) 모형”, 2020. 09.26 접속, Soft carpentry,  https://statkclee.github.io/statistics/stat-time-series-arma.html
- “ARIMA 총정리”, Challenge의 네이버 블로그, 2020.09.19 접속, 출처 https://blog.naver.com/nywoo19/221600142327
- “KBO리그 기록 및 순위＂ NAVER SPORTS 야구 기록/순위, https://sports.news.naver.com/kbaseball/record/index.nhn?category=kbo
- 제출자료 폰트: 나눔스퀘어, 네이버 한글한글 아름답게 