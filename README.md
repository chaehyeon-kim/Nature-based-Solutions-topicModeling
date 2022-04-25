## NbS(Nature-based Solutions) 연구 동향 분석

### 분석 주제 
nbs(Nature-based Solutions) 자연기반해법 활용 - 기후변화 대응을 위한 신림부문의 자연기반해법 활용 논문

### 분석 목표 
nbs 관련 논문의 연구 동향을 파악하고 이를 어떻게 국내 산림 분야에 응용할 수 있는지 결론 도출 

### 분석 방법 
- nbs 관련 논문 파악하여 분류 후 연도별 연구동향 분석 
- Topic Modeling : LDA
- Association Analysis


### 세부 

### 프로젝트 목적

자연기반해법에 대한 **연구 및 주요 주제**에 대한 관심에 대한 동향 분석

### 데이터 수집

- NbS를 관련 키워드에 포함하고 있는 논문들을 모집단으로 구축한 후 제목, 초록, 발행연도 등의 정보를 수집하여 NbS에 대한 그동안의 연구동향을 분석하고자 한다.

### 데이터 전처리
| 순서 |                                 과정 |                                                      비고  |
| --- | --- | --- |
| 1 | 한글, 숫자, 특수문자 등 제거  |  |
| 2 | 대문자 ⇒ 소문자  |  |
| 3 | 토큰화 및 품사 태깅 | (terrestrial, JJ), (wine, NN), (face, VBP),(a, DT) |
| 4 | 품사 형태 변경  | (terrestrial, a), (wine,n), (face, v) * 표제어 추출 input 형식에 맞는 품사 형태로 변경  |
| 5 | 표제어(Lemmaization) | (producers, n) → (producer, n) ,  (growing, v) → (grow, v) |
| 6 | 명사 추출  | 품사 ‘n’인 단어들만 추출  |
| 7-1 | 불용어 제거 - nltk 제공  | I my me mine all should a ...  |
| 7-2 | 불용어 제거 - NbS 제공  | 'nature', 'based', 'solutions', 'nbs', 'studing', 'studies', 'study' ,'management', 'manage', 'model', 'models', 'use', 'used', 'uses','plan', 'plans', 'planned', 'increase', 'increased', 'increases','service', 'services', 'result', 'results', 'resulted', 'system', 'systems', 'implement', 'implements', 'implementation', 'treat', 'treatment', 'treated', 'treats' |
| 7-3 | 불용어 제거 - DILab 제공|'change','area’,'city','approach','author','analysis','benefit','impact','effect','research','adaptation','planning','project','solution','challenge','development','journal','process','paper','nb’,'ecosystem', 'quality', 'method', 'level', 'article', 'data', 'value’ |
| 8 | TF-IDF 임계값 이하 단어 제거  | 전체 논문의 95%에서 등장하는 단어 제거 'others','twelve','amount','move','name','side','front','interest','latter','etc’ 등 총 60개 단어 제거  |
### 데이터 분석

1. 분할표
2. 키워드 추가 
- 연관분석 (장바구니 분석 - apriori)
- 연관어 분석 (동시 출현 기반, word2vec 기반)
3. 토픽모델링
- LDA(Latent Dirichlet Allocation): 전체 단어노드의 평균 TF-IDF는 284.40으로 본 연구에서는 TF-IDF 값 0.1을 임계치로 설정하여 이보다 큰 가중치 값을 갖는 단어들을 대상으로 LDA 분석에 활용
- Dynamic Topic Modeling
4. 동시 출현 기반 연관어 분석
- 중심성 계수 → 연결 중심성 / 매개 중심성 / 근접 중심성
- 1년 단위(2014년-2022년), 3년 단위(2014년-2022년), 4년 단위 분석(2011년-2022년)
5. 단순 빈도 분석 (HOT/COLD)
