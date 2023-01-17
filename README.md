# 신문사 성향 별 대한민국 정치흐름 파악
텍스트 데이터분석 전공 프로젝트

<br/>

## 1. 배경 & 목적

- 신문사 성향 별 사건 보도 시각 차이 파악
- 좌파, 우파 경향이 강한 신문사 별로 형태소 분석, 감정 분석, 주제 분석 등을 수행

<br/>

## 2. 주최/주관 & 팀원

- 주최/주관: AI빅데이터융합경영학과 전공 수업 ‘텍스트데이터분석’
- 팀원: 없음 (개인 프로젝트)

<br/>

## 3. 프로젝트 기간

- 2021.05. ~ 2021.06. (2개월)

<br/>

## 4. 프로젝트 소개

<img src='https://user-images.githubusercontent.com/75362328/213023758-d9fbbe6c-9819-40f9-a6ce-70690d54b387.png' width='100%' height='80%'>

&nbsp;&nbsp;&nbsp;&nbsp; 대표적인 우리나라의 신문사들의 성향에 대해 알아보고 **성향 별로 사건을 어떻게 다루는지 시각 차이**를 알아보는 프로젝트이다. 사설이 일반 기사보다 해당 신문사의 주장이나 의견을 더 잘 반영할 것이라고 판단하였기 때문에 성향이 뚜렷한 순서대로 9개의 신문사의 사설들을 **Selenium으로 크롤링하여** 수집하였다. 다양한 종류의 기사를 수집하기 위해 종합지뿐만 아니라 경제지와 인터넷뉴스를 포함하여 스크래핑 하였고, 그 결과 **보수 신문사는 조선일보, 중앙일보, 동아일보, 한국경제를 선정**하였고 **진보 신문사는 한겨례, 프레시안, 경향신문, 머니투데이, 이데일리를 선정**하였다.

&nbsp;&nbsp;&nbsp;&nbsp; 다양한 전처리 과정도 거쳤는데 **보수 신문사는 1, 진보 신문사는 0**으로 데이터 라벨링을 해주었다. **kiwi, konlpy, stanza** 패키지를 모두 사용해 본 결과 stanza가 가장 형태소 분석이 잘됐기 때문에 **stanza 패키지를 사용해서 형태소 분석**을 진행했다. 기사 제목을 스크래핑 한 것이기 때문에 명사만을 추출해서 **단어 문서 행렬**을 만들었다. 같은 내용을 다르게 보도하는 시각 차이를 보고자 하는 것이기 때문에 두 성향에 모두 많이 나오는 단어(정부, 국민, 대통령), 의미 없는 단어(것, 만, 년, 수, 때, 일, 차, 1, 2, 3), 잘못 분석된 단어(코로, 당코로), 기자 이름(오동희) 등을 **불용어 처리**해 주었다.

&nbsp;&nbsp;&nbsp;&nbsp; 감정 분석을 진행하기 위해 기존의 **CSR 방식과 COO 방식으로 실험**한 결과 **양의 가중치(보수)를 띄는 단어는 대표적으로 “文”, “與”, “정권”, “靑”, “조국”** 등으로 현 정부와 당을 지칭하는 단어가 많이 나왔고 **음의 가중치(진보)를 띄는 단어는 대표적으로 “합의”, “계기”, “실천”, “후퇴”, “실행”** 등으로 실제 행동하는 느낌의 단어가 많이 나왔다. 사설은 보통 비판하는 내용을 많이 쓰기 때문에 보수 쪽에서 진보 쪽을 비판하는 글을 많이 썼다는 것을 알 수 있다. 반면, 진보 쪽 언론사는 현재 정권을 지지하기 때문에 현재의 상황을 있는 그대로 보도하기 위해 위와 같은 단어를 많이 쓴 것으로 보인다. 감성 분석이 0과 1을 맞추는 문제이기 때문에 추가적으로 분류에 성능이 좋은 **MLPClassifier, SVC, DecisionTreeClassifier**도 사용해 모델을 돌려본 결과 **SVC 모델이 가장 좋은 성능**을 보였다.

&nbsp;&nbsp;&nbsp;&nbsp; **LSA와 NMF, LDA** 중 LSA에 회전을 적용한 뒤 해석하는 방법이 가장 뚜렷하게 의미를 도출해냈기 때문에 **LSA를 사용해서 주제 분석**을 하였다. 한 예시로 감성 분석에서 보수 쪽 성향이 뚜렷하게 나타났던 단어인 **“與(여)”을 가지고 주제 분석**을 해 본 결과 **“비리”, “불안”, “혈세”, “무능”, “참담”, “고집”** 등 매우 부정정인 단어들이 많이 나온 것을 확인 할 수 있었다. 또한 신문사 별로 “與”가 나온 비중을 살펴본 결과 조선일보, 동아일보, 한국경제 등 보수 쪽의 신문사에서 많이 나왔다는 것을 알 수 있다. 이 말은 보수성향의 신문사에서 여당을 매우 좋지 않게 평가 했다는 것을 의미한다.

<br/>

## 5. 프로젝트 담당 역할

- Selenium을 활용한 9개 신문사 사설 제목 크롤링
- Stanza 패키지를 사용한 형태소 분석 및 불용어 처리 (Kiwi, Konlpy 구현 및 성능 비교)
- CSR, COO 방식과 DNN 기법을 통한 감성 분석
- LSA를 사용한 주제 분석 (NMF, LDA 구현 및 성능 비교)

<br/>

## 6. 발표 자료

[텍데분 최종 발표자료](https://drive.google.com/file/d/11vEo-_S2sKjOxyrR75Gpm4UpOUoMPLMB/view?usp=sharing)
