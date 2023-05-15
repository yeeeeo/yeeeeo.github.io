---
title:  "전북대 빅데이터 분석경진대회 우수상 수상작" 
excerpt: "클러스터링과 회귀분석을 통한 공기 정화시스템 입지선정"

categories:
  - Project
tags:
  - [Analysis, Project]

toc: true
toc_sticky: true
 
date: 2023-02-23
last_modified_at: 2023-02-23

---

## 서울 지하철 '맑은' 공기 프로젝트 
### 클러스터링과 회귀분석을 통한 공기 정화시스템 입지선정

2022 전북대 통계학과 빅데이터 분석 경연대회에 **맑은 하늘**팀으로 출전하여 **3등상을 수상**받은 데이터 분석 및 시각화 프로젝트입니다.    
2022.01.10 ~ 2022.01.14, 약 4박 5일 해커톤 형식으로 진행했습니다.  

[프로젝트 코드 보관소](https://github.com/heoni00/2022-AnalysisCompetition-Subway)  
 
#### 참가인원 

고건우, 김차헌  

- 통계학, 정치외교학 학부 출신
- 프로그래밍, 머신러닝, 회귀분석, 데이터 분석, 시각화 등에 관심 및 일정 수준의 이해에 기반하여 분석 진행

#### 프로젝트 동기 및 목표 

본 프로젝트는 학습한 분석 기법 및 AI를 적용하고 분석 경험을 증진하기 위해 출전했습니다. 특히 서비스 개발이 아닌 **데이터 분석 및 인사이트 도출**에 중점을 두는 분석 프로젝트임에 의의가 컸습니다.    

원자료 가공, 데이터 수집 그리고 EDA 진행 그리고 적합한 알고리즘을 선택하여 인사이트를 도출하고 시각화 기법을 사용해서 전달하는 일련의 데이터 분석 프로세스 일체를 소수의 인원으로 빠른 시일 내에 완성하고 대회 수상을 목표로 했습니다.   

### OVERVIEW

![슬라이드1](https://user-images.githubusercontent.com/67791317/203099124-bc5fc6d9-f072-424a-ae54-cb8dca8e9da2.JPG)  

#### 연구 배경 

![슬라이드3](https://user-images.githubusercontent.com/67791317/203251191-4ee55691-1df7-4c22-9f89-a8256a9b1dc1.JPG)  

최근 미세먼지와 더불어 COVID-19으로 인해 공기질 및 개인 건강에 관한 관심이 높다. 지하철 정보 및 유동인구 그리고 공기질에 관한 데이터를 토대로 각 호선 및 역명에 따른 오염정도 및 상관관계 등의 정보를 분석하고 그 결과를 효과적으로 활용할 수 있는 방안을 찾았다.     

![슬라이드6](https://user-images.githubusercontent.com/67791317/203251222-72b27368-67ad-4f9a-b532-f33d056f0b94.JPG)  

진행중인 공기 정화 시스템의 설치를 제한된 비용내에 더 효과적으로 설치*운용할 수 있도록 클러스터링 및 회귀분석 알고리즘을 통해 **입지 선정 및 설치 순서**를 제안한다.     

#### 분석 프로세스 

![슬라이드5](https://user-images.githubusercontent.com/67791317/203252116-f9410009-766a-4c1b-a534-e91c76e14d81.JPG)

#### 데이터 목록

`-` 제공 데이터    
- Data1.csv : 지하철 혼잡도 정보 (호선, 역번호, 역명, 시간대별 혼잡도)  
- Data3.csv : 자치구별 지하철 역 정보 (호선, 자치구)  

`-` 공공데이터   
- 서울교통공사_역사건축정보_2020.csv : (역명, 연식 등)  
- 서울교통공사_역사심도정보_2020.csv : (역명, 심도 등)  
- 서울교통공사_월별승하차인원_2020.csv : (역명, 월별 승하차 인원 등)  
- 서울교통공사_환기구정보_2020.csv : (역명, 환기구 정보)  

`-` 가공데이터   
- 서울교통공사_역정보 -> 지하철 역 위도 경도 좌표   
- 서울교통공사 공기질 2020 -> 5가지 공기질 요소 데이터  

#### 데이터 전처리 

**데이터 프레임 생성**
1. 각 csv 파일을 데이터프레임으로 만든 뒤 필요없는 열을 제거, 결측치 대체 및 삭제합니다. 
2. 혼잡도와 승객수는 역별 평균값을 취하여 사용한다. 
3. 모든 데이터 프레임의 기본키를 ['호선','역명'] 형식으로 맞춘다. 
4. 기본키를 이용하여 최종 병합한다. 

**최종 병합된 DataFrame**

![image](https://user-images.githubusercontent.com/67791317/203371656-86f3693f-ae43-4bd0-8400-f6680b25295c.jpeg)

**공기질 데이터 변수 재조합**

1. 종합 공기질 점수를 계산하기 위해 5가지 척도를 종합하여 생성한다.   

```python
공기질척도 = (미세먼지 / 100) + (포름알데히드 / 100 )+ (초미세먼지 / 50) + (일산화탄소 / 10) + (이산화탄소 / 1000)
```

![image](https://user-images.githubusercontent.com/67791317/203579637-f51700ca-75b5-486e-9b5e-baeb971c2bd2.png)


2. 각 변수들의 영향력을 동일하게 하기 위해, feature scaling 진행 
3. Standard Scaler로 정규화 진행, MinMax Scaler를 통해 피쳐의 범위를 0~1 사이로 변환

#### 데이터 탐색 

**상관관계 탐색**

상관계수행렬을 만들어 공기질 점수와 상관관계를 파악하고 히트맵을 통해 시각화해 확인. 

<img width="456" alt="image" src="https://user-images.githubusercontent.com/67791317/203373835-0b5fc407-fabf-43dd-b617-4b7054d97052.png">

**지도 시각화**

folium 패키지를 활용하여 지하철역별 공기질과 승객수를 지도시각화하여 표현
원은 지하철 역을 나타내며, 원의 색이 빨갈 수록 공기질이 나쁘고 크기가 클 수록 승객수가 많다. 

<img width="632" alt="image" src="https://user-images.githubusercontent.com/67791317/203374381-a69ad6dc-bdcd-46ca-96d0-06ae695a9fa6.png">

#### 분석 모델 

K-mean 클러스터링을 통해 공기정화시스템 설치후보구역을 선정  

1. 클러스터링을 통해 변수 3개 (공기질점수, 평균혼잡도, 환승역개수)를 사용함. 
2. 해당 변수 우선수위는 공기질 점수 > 평균혼잡도 > 환승역개수로 설정함.   
3. K = 1 ~ 10 까지 놓고, 각 k-means clustering으로 얻은 모델의 군집내 총 제곱합을 plot함. 

<img width="441" alt="image" src="https://user-images.githubusercontent.com/67791317/203375193-fe9675de-f60e-4094-9639-8b2dc978fb8c.png">

4. plot이 감소하는 추세가 급격한 지점이 elbow point로 해당 지점을 군집의 개수로 사용. 
5. 각 군집별 변수 평균을 계산함. 

![image](https://user-images.githubusercontent.com/67791317/203579838-acf2e254-152e-4ad9-b2eb-5f049e92cdbe.png)

6. 0번 군집이 공기질 점수와 평균혼잡도와 환승역 개수가 크므로 0번 군집에 해당하는 역을 우선 설치군집으로 채택

#### 클러스터링 결과 시각화

<img width="562" alt="image" src="https://user-images.githubusercontent.com/67791317/203375817-f245e61a-c0dc-41cf-8a19-1e90abe8d918.png">

#### 회귀분석 (군집 내 우선순위)

공기질 척도를 사용하여 각 변수의 가중치를 생성 

```python
후보선정지수 = 0.1676 * 총승객수 + 0.1971 * 레일면고 + 0.1956 * 정거장깊이 + 0.1196 * 환기구 + 0.2820 * 연식
```
![image](https://user-images.githubusercontent.com/67791317/203375874-acdc0a79-fadc-459d-bb9f-17218f2b8523.jpeg)

#### 최종 결과 

회귀분석을 통해 가중치를 생산한 값을 적용하여 후보선정지수를 계산  
가장 지수가 높은 역 3개를 뽑아 최종 입지로 선정하였다. 

**1호선 서울역, 2호선 강남역, 2호선 시청역**  
![image](https://user-images.githubusercontent.com/67791317/203579982-8434df66-05f0-41d1-9a7c-a001d683740a.png)

### 레퍼런스 

#### 연구 배경 

- Web) 서울 교통공사 Webzine, 2022.01, http://webzine.seoulmetro.co.kr/enewspaper/articleview.php?master=&aid=1902&sid=73&mvid=692
- 기사) 심우섭, [리포트+] "안에서도 목이 칼칼" 실내 미세먼지 어쩌나 , SBS, 1, https://news.sbs.co.kr/news/endPage.do?news_id=N1005168647
- Web) 인천교통공사 ,https://www.ictr.or.kr/main/safety/environment/sense.jsp
- 논문) 한국환경사회정책연구소, ‘지하철역내 공기질에 대한 문제점과 개선방안 :3,’, 2003, Vol.2003.No.4, 539, 39~48

#### 데이터 참고 

- Web) 서울교통공사 공공데이터 제공, http://www.seoulmetro.co.kr/kr/board.do?menuIdx=551

#### 코드 

- Stack overflow
- Web) 데 박, https://blog.naver.com/111ambition/222503252689
- Web) 테디코드, https://teddylee777.github.io/visualization/folium