## TeamProject_AI_Food_Recommendation_System

2020년도 대학교에서 수강한 산합혁력 프로젝트수업에서 진행된 프로젝트입니다.

Microsoft 본사 심재은 DataScientist께서 멘토를 맡아주셨습니다. 또한 이희연 지도 교수님이 FeedBack 해주시고 도와주셨습니다.

팀원은 김현명, 한도훈, 마위잉, 신희을, 김배승씨로 구성이 되었고 저는 그중 팀장의 역할을 맡아서 진행했습니다. 팀 이름은 산학클라쓰입니다.


## 프로젝트 개요

  코로나로 인해서 음식 자영업자 분들이 많이 힘들어지기도 했고 그에 따라 음식과 관련하여 배달앱 서비스 등등이 중요해지던 시기였습니다.
  
 이에 따라 우리 산학클라쓰팀은 음식 배달 Data를 통해 AI/ML을 구축하고 서비스 모델을 만들어보기로 하였습니다.
 
 다만 국내에선 배달 Data를 얻기가 힘들었고 직접 설문조사 하기에는 데이터 수와 자원이 부족했습니다. 노력 끝에 중국유학생분의 도움으로 중국의 빅데이터 시스템을 활용할 수 있었습니다. 중국 '우한'지역의 12지역에 대해서 위도,경도를 중심으로 모이는 배달 주문데이터를 '직접' 수집 및 전처리해서 사용하였습니다. 프로젝트 주제는 ‘음식 자영업자 분들을 위한 특정 지역별로 선호되는 음식종류 및 메뉴 추천 서비스’로 선정되었고 이를 통해 신규 요식업 창업자분들이나 신메뉴 개발을 고민하는 사업자분들게 도움을 주고자 하였습니다.


## 진행 기간
2020-03-02 ~ 2020-06-20


## 프로젝트 구성

 우리의 프로젝트 단계는 크게 데이터 추출 – 추천시스템 모델 개발 – 추천시스템 개선(TextMing 적용) - 통계치 추출 및 분석, 사용성 평가의 단계로 이루어진다.
그중 데이터 추출부분부터 알아보겠습니다.

## 데이터 추출
(마위잉씨가 주로 맡게된 역할입니다.)
![image](https://user-images.githubusercontent.com/44837403/115152128-d1d1bc80-a0aa-11eb-858d-6159df836203.png)

iDataAPI(광저우간혁신정보과학기술유한공사)는 중국에서의 한 데이터 서비스 공급업체로 2014년 창립 이후 기업, 기구, 개인에게 전문적인 데이터 수집, 데이터 융합, 데이터 분석과 데이터 관리 등 서비스를 지속적으로 제공해왔습니다. 우리 산학클라쓰팀의 마위잉씨의 도움으로 위의 업체에서 배달 주문데이터에 대해서 수집하고 활용할 수 있었습니다.

 ![image](https://user-images.githubusercontent.com/44837403/120885843-fadfe980-c625-11eb-867e-6a8e50857d6c.png)

 산학클라쓰팀에서는 위의 우한지역 1 ~ 11번 지역 중 1 ~ 9번 지역에 대해서 모이는 배달 주문데이터를 활용하였습니다. 

![image](https://user-images.githubusercontent.com/44837403/115152381-cf239700-a0ab-11eb-88a5-b8a962dbb7d0.png)


위와 같이 데이터를 구조화하고 정리해서 사용했습니다.

## 추천시스템 모델 개발

 추천시스템 모델은 아나콘다 – Jupiter Notebook 환경에서 Python언어를 사용해서 구축하였습니다. 이는 심재은 멘토님의 조언과 더불어 다른 DataScientist의 블로그, 깃허브 등을 참고를 했습니다. 구축된 모델의 전체적인 구조, 핵심 알고리즘은 아래와 같습니다. 


## 시스템 진행도

![image](https://user-images.githubusercontent.com/44837403/121030985-edbd2900-c7e4-11eb-9096-1f9d5ac6229c.png)

추천시스템은 위와 같은 Flow를 가지게 됩니다.


## 핵심 알고리즘과 기법

#### Data Normalization
![image](https://user-images.githubusercontent.com/44837403/121035624-062f4280-c7e9-11eb-9013-792b224e7b69.png)


Data Normalization 과정을 해주는 부분입니다. 위에서 보면 알겠지만 기존의 평점들은 0점이 매겨진 경우가 있습니다. 이 경우는 기존 사용자들이 전 영역의 메뉴를 평가하지 않기 때문에 발생합니다. 이를 그대로 사용하면 모델이 평점을 가지는 데이터(약3.5의 평점)에 Over Fitting되는 문제들이 발생될 수 있기 때문에 각 평점들에 평균 평점을 빼주는 작업을 진행하였습니다.


#### 핵심 알고리즘

평점들이 매겨진 데이터들을 Matrix Factorization을 적용하였습니다.

![image](https://user-images.githubusercontent.com/44837403/121035712-1d6e3000-c7e9-11eb-88d0-cc50675d0799.png)

 위 알고리즘을 사용하게 될 경우 가지는 장점은 다음과 같습니다.
 
 첫 번째는 잠재요인의 특성들을 추출하고 이를 통해 모델을 구축하면서 데이터의 공간을 효율적으로 사용하게 됩니다. 이는 빅데이터를 사용하는 추천시스템 특성상 실용성이 더해지는 특성입니다.
 
 두 번째는 다차원의 데이터 특성을 가지는 데이터가 저차원의 행렬들로 나누어졌다가 다시 복원하는 과정을 거치면서 기존에 채워지지 않았던 다른 평점 부분들도 채워지게 된다. 이를 nearest neighbor collaborative filtering(최근접 이웃 기반)이라고도 합니다.
 
 세 번째는 사용자가 음식메뉴에 매기는 평점들을 기반으로 한다는 것입니다. 
기존의 content-based filtering에서 Item을 위주로 단순히 평가를 하는 것이 아니라 사용자의 행동양식이 들어간다는 점에서 신뢰성을 더 부여하게 됩니다.


### 지역별로 음식메뉴에 대해 가지는 선호도 Heat Map

![image](https://user-images.githubusercontent.com/44837403/115152557-8b7d5d00-a0ac-11eb-92c2-52cf7cdf6a6a.png)


## 최종 추천 리스트
![image](https://user-images.githubusercontent.com/44837403/115152578-a18b1d80-a0ac-11eb-8f5f-b2d8796a14cd.png)


## 추천시스템 모델 개선

#### Text Mining에 기초한 가중치 부여

 기존의 추천시스템 모델을 더욱 더 개선하고자 노력하였습니다. 그래서 모아지는 데이터 중 리뷰 데이터를 이용해서 TextMining을 이용한 가중치 부여를 하기로 하였습니다.
가중치로 사용된 데이터는 goodtag(좋은 평가)와 ratingCount(별점 수)입니다.

![image](https://user-images.githubusercontent.com/44837403/115152725-3beb6100-a0ad-11eb-9b7b-54c9d2e6ae2f.png)


참고링크
http://www.ndsl.kr/ndsl/commons/util/ndslOriginalView.do?dbt=JAKO&cn=JAKO201913747259432&oCn=JAKO201913747259432&pageCode=PG11&journal=NJOU00400536

![image](https://user-images.githubusercontent.com/44837403/115152730-43ab0580-a0ad-11eb-9cf8-049c3bf47a48.png)


 위는 ‘평점과 리뷰 텍스트 감성분석을 결합한 추천시스템 향상 방안 연구’ 입니다. 이는 영화 추천시스템에서 사용자들의 리뷰가 가지는 긍정적인 감성수치와 부정적인 감성수치를 바탕으로 가중치를 MF기법에 더해주는 방안에 대해서 연구한 논문입니다. 논문에서는 줄어든 MAE를 근거로 TextMining의 효과에 입증을 더해주었습니다. 이에 우리 산학클라쓰팀 역시 위와 같은 방식으로 가중치를 더해주었습니다.


## 프로젝트 서비스 제공 및 사용성 평가

#### 프로젝트 서비스 제공

 우리 산학클라쓰팀은 구축된 추천시스템을 통해서 추출해낼 수 있는 통계치들을 비교 분석하고 이를 제공하였습니다. 음식 자영업관련하여 신메뉴개발을 고민하는 사업자분들, 창업을 고려하는 사람들에게 있어서 도움을 줄 수 있는 서비스를 제공하였습니다.
 
![image](https://user-images.githubusercontent.com/44837403/115152841-da77c200-a0ad-11eb-8bd5-6e699939683e.png)


#### 사용성 평가(네이버 폼)

최종 프로젝트의 사용자 만족도 평가를 위해 네이버폼을 이용해 인터뷰를 진행하였습니다. 유용성, 사용성, 개성 총 3가지 카테고리로 분류하여 조사를 진행하였고 각 질문 별로 1부터 5까지 만족도를 선택할 수 있도록 하였습니다. 

![image](https://user-images.githubusercontent.com/44837403/115152953-6ab60700-a0ae-11eb-9980-e67b1ec359e9.png)



## 느낀점

 AI/ML에 대해서 배울 수 있는 좋은 프로젝트 였습니다. 멘토분, 지도교수님, 여러 팀원들의 도움으로 AI/ML모델을 만들었습니다.
 데이터들도 프로젝트 주제에 맞게 직접 수집, 전처리해서 모델에 적용하였습니다.

팀장을 맡게 되면서 팀원들의 장점과 능력을 이해하고 이에 맞게 역할 분배하는 것이 중요하다는 것을 꺠달았습니다. 각 팀원분들은 각자가 가진 장점들이 있고 역할이 분배 되었을 때 이를 확인할 수 있습니다. 또 전체적으로 팀이 좋은 방향으로 나아갈 수 있도록 프로젝트의 방향성을 계속해서 신경썼습니다.

  AI모델을 만들때에는 사용되는 데이터의 특징과 이 데이터들이 모델에 어떻게 작용되는지를 생각해보는 것이 중요하다는 것을 느꼈습니다. 질 좋은 데이터들을 최대한 많이 모을 수 있어야 하고 프로젝트 주제에 맞게 이 데이터들을 전처리해 모델에 적용을 해주어야 합니다. 그 과정에서 모델의 성능을 개선시킬 수 있는 여러 방법과 기법들을 찾아보았습니다. 이를 통해 사람들에게 있어서 더 좋은 서비스가 되는 모델을 만들고자 노력했습니다.







