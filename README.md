# Study-on-Detecting-Driver-s-Abnormal-Behavior-for-Safer-Autonomous-Driving

운전을 해봤던 사람이라면 한번쯤 졸음운전으로 가슴이 출렁했던 경험이 있을 것이다. 2015년 교통안전공단 조사에 따르면 고속도로 운전자 10명중 4명은 졸음운전을 경험한다고 발표했고, 인명사고는 음주운전보다 정도가 심하며 전체 사고의 36.7%가 졸음운전에서 비롯된다고 한다. 본 연구는 졸음운전과 같이 운전 도중 발생할 수 있는 운전자 부주의 (Human Error) 문제에 인공지능 기술을 접목하여 실현가능한 해결책을 제시할 수 없을까 하는 고찰에서 시작되었다.<br/>

<br/>

## 학습 데이터 구축

운전자의 이상행동 감지를 위해 운전자가 취하는 특징적인 행동 패턴이 포함된 데이터를 필요로 한다. kaggle의 “State Farm Distracted Driver Detection" 데이터 셋을 사용하여 10가지의 행동 패턴을 분류하고, 데이터 셋에 포함되지 않은 졸음운전 상태의 행동 패턴 데이터를 추가하여 총 11가지의 상태를 감지할 수 있게 한다.<br/>
<br/>
State Farm Distracted Driver Detection 데이터 셋에 포함된 10가지 클래스는 다음과 같다.
 - c0 : 안전 운전
 - c1 : 문자 메시지 - 오른쪽
 - c2 : 전화 통화 - 오른쪽
 - c3 : 문자 메시지 - 왼쪽
 - c4 : 전화 통화 - 왼쪽
 - c5 : 라디오 작동
 - c6 : 음주
 - c7 : 뒤로 손을 뻗는 행위
 - c8 : 머리 손질 및 메이크업
 - c9 : 승객과 대화<br/>
추가적으로 c10 : 졸음 운전 클래스를 생성했다.<br/>
<br/>

State Farm Distracted Driver Detection 데이터 셋 이미지의 크기는  640 x 480 pixel로  차량안의 운전자가 운전을 하며 각각의 특징적인 행동을 취하는 장면이 포함되어 있다.
추가하는 졸음 운전상태의 데이터 또한 640 x 480 pixel 사이즈의 이미지로 진행했다. <br/>

![image](https://user-images.githubusercontent.com/69569278/163129770-db3f4d73-6710-40d1-9fa9-1b4ed7a40e9d.png)
![image](https://user-images.githubusercontent.com/69569278/163129833-bfb08a87-a189-4df3-9cbf-984535877a37.png)
![JnI0dF4lh_CkDeSuk2vAvZHxHtqZjsQCi3CM5qYxhrT1jTKtW4qfEdvQESWB1J32-C46KL-G6iJmVrJ0OVsRINZretG9yecqY-gvy-ovMmKBxY8B2271oxAdMieW](https://user-images.githubusercontent.com/69569278/163130395-9d817297-89ac-4ec6-b1fc-99f7d17adbfb.png) <br/>
<br/>

## 모델 선택 및 성능 평가

densenet과 resnet50, resnet152, squeezenet 모델을 사용하여 11종의 운전자 행동 패턴 데이터를 각각 학습시켜보았다.<br/>
densenet의 경우 validation accuracy가 96%, validation loss는 0.2129 의 가장 우수한 성능을 보였다. densenet의 pretrained모델을 전이학습 시킨 경우에도 val_acc 96%로 비슷한 결과를 보였다.<br/>
<br/>
![image](https://user-images.githubusercontent.com/69569278/163131013-81a0663a-3c61-4b41-8f1c-d3b8afc4c7e1.png) <br/>

|모델|Val_Acc|
|:---|:---:|
|densenet|**96%**|
|densenet transferlearning|**96%**|
|resnet50|51%|
|resnet50 transferlearning|54%|
|resnet152|27%|
|resnet152 transferlearning|26%|
|squeezenet|54%|
|squeezenet transferlearning|40%|

<br/><br/>
