# DSL-23-1-modeling-Bicycle_Demand_Prediction
서울시 공공자전거 따릉이 대여량 예측 모델링(RNN)

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FDataScience-Lab-Yonsei%2F9th_EDA%2F1%25E1%2584%258C%25E1%2585%25A9&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)



#### 참여자 : 도승범, 심은조, 유희조, 임세민, 정주영
## 모델링 프로젝트 자료 소개
> * data
>   * [서울특별시 공공자전거 대여이력 정보](https://dacon.io/competitions/official/235980/data) : 따릉이의 반납 및 대여 정보
>   * [서울특별시 공공자전거 이용 정보](http://data.krx.co.kr/contents/MDC/MAIN/main/index.cmd) : 따릉이 이용자들의 연령대, 성별, 정기권 이용여부 등 유저 정보
>   * [nasdaq_data.csv](https://kr.investing.com/indices/nasdaq-composite) : 날씨 데이터
>   * [S&P_data.csv](https://kr.investing.com/indices/us-spx-500) : 지하철 이용량 데이터
> * preprocessing
>   * [1_Data_Merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
>   * [2_train_test_split_v2.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/2_train_test_split_v2.ipynb)
>   * [3_live_work_clustered.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
>   * [4_weather_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
>   * [5_subway_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
>   * [6_regular_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
>   * [7_teen_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb)
> * modeling
>   * [RNN_final.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/modeling/RNN_final.ipynb)
> * PPT

<br>


## EDA 프로젝트 요약

1. 데이터 소개

        - kospi_data.csv : KOSPI의 일간 등락, 종가, 시가 등의 정보를 담고 있는 데이터
   
2. 데이터 전처리

        - 주가 시계열 자체의 비정상성을 감안하여, 로그 차분을 통해 정상시계열화(수익률 시계열)
 
3. 분석 방법 및 결과
    
        - 1월효과, 연말효과, 서머랠리, 월요일효과 등 주식시장의 이례현상(Anormalies) 존재 여부 가설 검정
        - 존재한다고 검정된 이례현상에 대하여 경제학/경영학 이론 기반 가설 제시
        - 설명가설의 타당성 검토하기 위한 통계적 검증
    
4. 결론

        - 월요일효과 존재: 금요일 장마감 이후 축적된 미반영 정보들에 의해 월요일 시장의 변동성 증가, 월요일 주가 수익률 하락 압력
        - 연말효과 존재: 연말 경기 호조에 따른 주가 상승 압력과 절세전략 및 배당금 효과에 의한 주가 등락의 전형적 패턴 존재
        - 1월효과 존재: 연말 주가 하락에 따른 기저효과에 기인, 특히 개인투자자 영향력 큰 코스닥에서 더 뚜렷한 패턴 발견
        - 서머랠리 존재: 3분기 반도체 산업 호황에 대한 선반영, 상반기 양호한 수익률에 기반한 기관투자자들의 낙관주의
    
5. 아쉬운 점
    
        - 존재하는 이례현상들에 대하여 부분적인 설명만 제시할 뿐, 완벽한 설명으로는 부족함

6. 추가로 하면 좋을 분석 방법
    
        - 분석에서 다룬 이례현상들을 기반으로, 실제 투자 수익을 거둘 수 있는지 백테스팅
<br>

