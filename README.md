# 제4회 2023 연구개발특구 AI SPARK 챌린지 - 공기압축기 이상 판단
- 산업용 공기압축기의 이상 유무를 비지도학습 방식을 이용하여 판정
- 비정상적인 lable이 존재하지 않는 데이터의 Anomaly Detection
<br>

**데이터** <br>
<img width="732" alt="스크린샷 2023-08-01 오후 5 00 07" src="https://github.com/kwonkw/Air_Compressor_Abnormality/assets/131172214/97fbac40-0089-4d80-b2ab-15dc5729a99f">
- [https://aifactory.space/competition/data/2226]
<br>

**평가** <br>
<img width="461" alt="스크린샷 2023-08-01 오후 5 00 42" src="https://github.com/kwonkw/Air_Compressor_Abnormality/assets/131172214/35bf6dec-eb58-49e5-8e16-eda7b1f39c7c">
- 심사 기준: F1-Score
- Scikit-Learn에 내장된 F1-Score를 ‘macro’ 옵션으로 설정하여 평가에 사용
- Macro F1-Score
  - 분류 모델에서 사용되는 머신러닝 평가지표
  - class와 label의 각각 F1-score를 계산한 뒤 평균내는 방식
  - F1-Score는 0.0 ~ 1.0 사의의 1에 가까울수록 좋음
  - Macro-F1점수는 클래스별/레이블별 F1-score의 평균
<br>

**사용 툴**
- Google colab
<br>

**최종 결과 및 성과**
- Macro F1-score 최종 0.9535302503점
<br>
<br>

## 해결방안
### 1. 파생변수 생성 <br>
1) hp 
2) 회전력(Torque) = 9.55 x 모터전류(Motor Current) x 모터RPM(Motor RPM)
3) 유효출력(Power) = 회전력(Torque) x 2 x π x 모터RPM(Motor RPM) / 60
4) 열효율(Thermal Efficiency) = (입력공기온도 - 출력공기온도) / 입력공기온도

### 2. 정규화
- 직접 정상범위 설정 후 데이터 정규화
  
### 3. 주성분분석(PCA)
- explained_varience_ratio를 확인한 결과 n_component를 2로 설정

### 4. 사용 변수 추출
- 'Month'
- 'Origin_State'
- 'Origin_Airport'
- 'Destination_State'
- 'Destination_Airport'
- 'Distance', 'Airline'
- 'Total_Time'
- 'dep_hour'
- 'arr_hour'
- 'Tail_Number'
- 'Delay'

### 5. 비지도 학습
**LocalOutlierFactor** <br>
   - 비지도학습이므로 지도학습에 사용되는 GridSearch, RandomSearch 사용하지 않음 <br>

**최종 결과 및 성과**
- F1-Score 최종 0.9535302503
<br>
<br>
