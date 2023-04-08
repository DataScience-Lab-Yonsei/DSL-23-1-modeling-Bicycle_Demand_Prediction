# DSL-23-1-modeling-Bicycle_Demand_Prediction
서울시 공공자전거 따릉이 대여량 예측 모델링(RNN)

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FDataScience-Lab-Yonsei%2F9th_EDA%2F1%25E1%2584%258C%25E1%2585%25A9&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)



#### 참여자 : 도승범, 심은조, 유희조, 임세민, 정주영
## 모델링 프로젝트 자료
> * data
>   * [서울특별시 공공자전거 대여이력 정보](http://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do#) : 따릉이의 반납 및 대여 정보
>   * [서울특별시 공공자전거 이용 정보](http://data.seoul.go.kr/dataList/OA-15245/F/1/datasetView.do) : 따릉이 이용자들의 연령대, 성별, 정기권 이용여부 등 유저 정보
>   * [서울특별시 공공자전거 대여소 정보](http://data.seoul.go.kr/dataList/OA-13252/F/1/datasetView.do) : 따릉이 대여소의 위치 정보
>   * [방재기상관측](https://data.kma.go.kr/data/grnd/selectAwsRltmList.do?pgmNo=56) : 관측소별 날씨 데이터
>   * [서울교통공사 승하차인원](https://www.data.go.kr/data/15099330/fileData.do) : 지하철 이용량 데이터
> * preprocessing
>   * [1_Data_Merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/1_Data_Merged.ipynb) : 월별 데이터 통합
>   * [2_train_test_split_v2.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/2_train_test_split_v2.ipynb) : train set과 test set 분리
>   * [3_live_work_clustered.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/3_live_work_clustered.ipynb) : 생활지구와 업무지구 분리 후 클러스터링
>   * [4_weather_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/4_weather_merged.ipynb) : 날씨 데이터 결합
>   * [5_subway_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/5_subway_merged.ipynb) : 지하철 이용량 결합
>   * [6_regular_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/6_regular_merged.ipynb) : 정기권 이용비율 결합
>   * [7_teen_merged.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/preprocessing/7_teen_merged.ipynb) : 10대 이용비율 결합
> * modeling
>   * [RNN_final.ipynb](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/modeling/RNN_final.ipynb)
> * PPT
>   * [PPT](https://github.com/SeungbeomDo/DSL-23-1-modeling-Bicycle_Demand_Prediction/blob/main/ppt/A%EC%A1%B0_PPT_%EC%B5%9C%EC%A2%85.pdf)

<br>


## 모델링 프로젝트 요약

### 1. Task 소개 
        - RNN을 활용한 따릉이 대여소 간 분배 작업 효율화 
        - RNN을 활용한 대여소별 따릉이 수요량 예측
        - 2021년 5,6,7월 대여소별 이용량 데이터를 사용해 2022년 5,6,7월 대여소별 이용량 예측 
   
### 2. 데이터 전처리 <br>
        - 2021년 train set, 2022년 test set 
        - 출퇴근 이용자의 비율이 높은 점을 감안하여, 대여소를 업무지구와 생활지구로 분류 
                - 출퇴근시간대 이용량이 그 외 시간대 이용량보다 유의하게 높은 경우 업무지구로 분류 
        - 이용자들은 한 곳의 대여소만을 이용하지는 않는다는 점을 감안하여, 위치기준 k-means 클러스터링 
                - 클러스터별 예측 과제로 전환 
        - 이용자들의 이용 과정에서 자연스럽게 분배가 이루어지는 점을 감안하여, 순대여량 칼럼을 생성
                - 순대여량 = 대여량 - 반납량을 주 y변수로 설정
 
### 3. 모델링
    
        - many-to-one RNN: 이전 시간대들의 순대여량 시퀀스로 예측 시간대 순대여량 예측
               - LSTM cell, number of stacked layers = 2, sequence length = 10, hidden size = 400, number of fc layers = 2
        - prediction range = 3(시간)
               - 예측 후 실제 분배 과정에 소요되는 시간 감안하여 3시간 후를 예측
        - window sliding
               - 실제 분배과정에서는 따릉이 정보가 실시간 업데이트되는 점을 반영하기 위해, train/test에서 window sliding 방법 사용
        - 2021년과 2022년 사이에 직장인들의 따릉이 이용량 급증
               - 출퇴근 시간대에서 성능 차이가 심한 것을 확인
               - 정기권 이용비율을 직장인 비율의 대리변수로 사용 + 예측시간대에 출퇴근시간대인지 여부(binary 변수) 추가
               - 순대여량 시퀀스의 RNN 히든 스테이트에 위 두 변수를 곱한 후 fc layer 적용
![image](https://user-images.githubusercontent.com/108214382/230713472-278062f7-1882-487d-ac39-b7fead3910c9.png)

    
### 4. 성능

        - Test set RMSE: 4.86
        - 출퇴근시간대 예측력 확보

![image](https://user-images.githubusercontent.com/108214382/230713303-ed2102eb-a347-4da9-ad10-d0e660caff7e.png)


    
<br>

