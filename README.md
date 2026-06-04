# 💊 약물 공동처방 네트워크 분석 (Analysis of Drug Co-prescription Network)

<br/>

<div align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/NetworkX-4B5EFC?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Gephi-4B5EFC?style=for-the-badge&logo=databricks&logoColor=white"/>
</div>

## 📌 1. 프로젝트 개요 (Overview)
* [cite_start]**배경:** COVID-19 장기화로 인해 우울 위험군 및 항우울제 처방 건수가 해마다 급증하고 있습니다[cite: 13, 14, 18]. [cite_start]기존 연구들은 단일 약품 처방 패턴 분석에 머물러 있어, 약물 간의 '공동 처방' 구조와 그에 따른 잠재적 약물 상호작용(DDI)의 맥락을 파악하기 어려웠습니다[cite: 20, 21].
* [cite_start]**목표:** 1. 2017년~2021년 한국 환자들의 **항우울제 공동처방 네트워크 구조의 시시각각 변하는 시계열 추이(COVID-19 전후) 분석** [cite: 26, 32]
  2. [cite_start]연령대별 우울증 유무에 따른 **만성질환 네트워크(Community Structure) 대조 분석 및 임상적 시사점 도출** [cite: 34, 35]

## 📊 2. 데이터셋 및 전처리 (Data & Preprocessing)
* [cite_start]**데이터 소스:** 국민건강보험공단 의약품 처방정보 (5개년, 연도별 무작위 100만 명 샘플 데이터) [cite: 140, 141, 142]
* **전처리 핵심:**
  * [cite_start]분절된 주성분 코드(9자리) 대신 약물의 주성분을 명확히 정의하기 위해, 세계보건기구(WHO) 기준의 **ATC 코드** 매핑 기준 데이터 구축 [cite: 132, 133, 148, 151]
  * [cite_start]하나의 주성분 코드가 다중 ATC 코드로 매핑된 데이터 오류를 정교하게 클리닝 처리 [cite: 153, 154]
  * [cite_start]타겟 분석을 위해 항우울제(N06A 계열) 및 주요 만성질환 관련 ATC 코드를 정밀 스크레이핑하여 최종 데이터프레임 구성 [cite: 190, 326, 328]

## 🔬 3. 핵심 분석 방법론 (Methodology)
* [cite_start]**거시적 네트워크 지표 분석 (Macroscopic Analysis):** 밀도(Density), 평균 차수(Mean Degree), 전이성(Transitivity), 차수 분포(Degree Distribution) 연도별 추적 [cite: 39]
* [cite_start]**중심성 지표 분석 (Centrality Analysis):** Degree, Eigenvector, Betweenness Centrality 비교 분석을 통한 네트워크 내 가교 약물(Bridge Drug) 식별 [cite: 48, 49, 52, 54]
* [cite_start]**확률적 블록 모델링 (Stochastic Block Modeling, SBM):** 처방 데이터 내에 잠재된 질환 커뮤니티 구조를 통계학적으로 파악하여 블록 간 상호작용 확률 연산 [cite: 99, 100]

## 💡 4. 연구 목적별 핵심 인사이트 (Key Findings)

### 📈 연구목적 1: COVID-19 전후 항우울제 공동처방 네트워크의 시계열 변화

* **네트워크 연결성 및 밀도의 지속적 증가**
  * [cite_start]팬데믹 기간을 거치며 네트워크의 Edge(엣지) 개수, Density(밀도), Mean Degree(평균 차수)가 전반적으로 우상향하는 추세를 기록했습니다[cite: 41, 44].
  * [cite_start]이는 코로나19 확산 전후로 환자들에게 처방되는 항우울제 약물들의 공동처방 빈도가 증가했으며, 처방 내역의 조합이 한층 다변화되고 밀집되었음을 증명합니다[cite: 42, 45].
* **Transitivity(전이성) 상승과 처방 프로토콜의 표준화**
  * [cite_start]시간이 흐를수록 노드 간 삼각형 형성 비율을 뜻하는 Transitivity 지표가 점진적으로 우상향했습니다[cite: 42, 224].
  * [cite_start]이는 항우울제 처방 시장 내에서 특정 약물 그룹들이 동시 처방되는 경향이 강화되었으며, 임상 현장에서 표준화된 병용 처방 프로토콜이 점차 정착되고 있음을 시사합니다[cite: 226, 227].
* **중심성 분석을 통해 발견한 핵심 매개 약물의 세대교체**
  * [cite_start]**플루복사민(N06AB08)의 약화와 티아넵틴(N06AX14)의 부상:** 2017년 처방 네트워크에서 플루복사민은 낮은 Degree 대비 높은 Betweenness Centrality를 보이며 강력한 가교(Bridge) 역할을 수행했으나, 2019년 이후 이 가교 역할이 유사한 임상 효능을 지닌 티아넵틴으로 점차 대체되는 뚜렷한 처방 패턴 변화가 관찰되었습니다[cite: 65, 69, 70, 71].
  * [cite_start]**에스시탈로프람(N06AB10)의 역할 축소:** 표준 항우울제로 널리 사용되며 높은 가교 중심성을 지녔던 에스시탈로프람은 2018년 이후 Betweenness Centrality가 점차 감소했습니다[cite: 73, 74, 75]. [cite_start]이는 임상적 부작용 이슈가 부각되면서 MAOI 그룹 등 타 항우울제와의 병용 처방이 제한된 결과가 네트워크 구조에 고스란히 반영된 것으로 해석됩니다[cite: 76, 77].

---

### 🧓 연구목적 2: 우울증 여부 및 연령에 따른 만성질환 네트워크 대조 분석

* **고령층 우울증 환자의 복합만성질환 발병 위험성 확인**
  * [cite_start]연령대별 Density(밀도) 변화를 분석한 결과, 비우울증 집단에 비해 우울증 집단에서 연령 가중치에 따른 네트워크 밀도가 현저히 큰 폭으로 상승함을 확인했습니다[cite: 83]. 
  * [cite_start]이는 우울증이라는 정신질환이 고령층 환자군에 이르러 단순 단일 질환에 머무는 것이 아니라, 다발성 복합만성질환(Multimorbidity)의 발병 확률 및 중증도 심화와 긴밀한 임상적 연관성이 있음을 통계적으로 시사합니다[cite: 84].
* **약물 상호작용 증가로 인한 커뮤니티 경계 모호화 (Modularity 감소)**
  * [cite_start]연령이 증가할수록 우울증 환자군의 만성질환 네트워크 내 모듈성(Modularity) 지표가 급격히 감소하는 경향이 관찰되었습니다[cite: 85].
  * [cite_start]이는 나이가 많아질수록 우울증 환자들에게 처방 약물 간 상호작용이 증가하여 개별 질환 약물군 간의 독립적인 커뮤니티 경계가 흐려지고 거시적인 네트워크 구조가 하나로 복잡하게 병합되는 현상을 반영합니다[cite: 86, 87].
* **우울증과 인지 기능 저하(치매)의 높은 상관성 발견**
  * [cite_start]중년층 및 고령층 우울증 네트워크에서 치매 치료 약물군(노란색 노드)이 압도적으로 높은 Degree Centrality(차수 중심성)를 기록했습니다[cite: 93, 94].
  * [cite_start]이는 우울증 환자들 중 다수의 환자가 치매 약물을 함께 처방받는 경향이 있음을 파악한 결과입니다[cite: 95]. [cite_start]우울증 환자에서 인지 기능 저하가 동반될 가능성이 크며, 치료 과정에서 치매 관련 약물 처방이 증가하는 유의미한 상관관계를 시각적으로 증명합니다[cite: 96, 97].

## 🚀 5. 프로젝트 한계 및 발전 방향 (Limitations & Future Work)
* [cite_start]**데이터 한계 극복:** 본 분석은 항우울제 처방 내역을 우울증 진단의 대리 변수로 활용하여 실제 환자의 진단 코드(ICD)를 정확히 확인하지 못했습니다[cite: 470]. [cite_start]향후 실제 진단 정보 데이터가 확보된다면 더 정교한 분석이 가능합니다[cite: 472].
* [cite_start]**방향성 네트워크 및 이질적 정보 네트워크(HIN)로의 확장:** 본 프로젝트는 처방전 연관 관계 기반의 무방향성(Undirected) 네트워크에 국한되었으나[cite: 476, 477], 향후 환자-의사-질병-약물을 모두 포함하는 다중 관계 중심의 **이질적 정보 네트워크(Heterogeneous Information Network, HIN)**로 모델링하고, **GNN(Graph Neural Networks)**을 활용한 고도화된 예측 모델로 발전시킬 수 있습니다.

## 🧠 6. 느낀점 및 회고 (Retrospective)
* **도메인 데이터 매핑을 통한 전처리 역량의 성장**
  * [cite_start]공공 데이터셋 특성상 주성분 코드가 복잡하게 분절되어 있어 초기 네트워크 노드 구성에 어려움이 있었습니다[cite: 149, 150]. [cite_start]이를 해결하기 위해 국제 분류 체계인 ATC 코드를 크로스 매핑하고 정제하는 과정을 거치면서[cite: 148, 154], 원천 데이터의 공백을 도메인 지식을 활용해 해결하는 데이터 엔지니어링적 접근의 가치를 깊이 깨달았습니다.
* **통계적 네트워크 과학이 가진 시각적 인사이트의 가치**
  * [cite_start]단순한 표 형태(Tabular Data)의 빈도 분석만으로는 파악하기 어려웠던 약물 간의 다각적 상호작용과 환자군 간의 거시적 구조 차이를 Gephi 시각화와 확률적 블록 모델(SBM), 중심성 지표를 통해 한눈에 증명해낼 수 있었습니다[cite: 48, 79, 99]. 데이터 속에 숨겨진 '관계의 구조'를 정의하는 네트워크 분석의 강력함을 체감했습니다.
* **향후 연구 모델 확장 및 기술적 지향점**
  * 이번 프로젝트에서 다진 그래프 데이터 핸들링 및 네트워크 분석 경험을 발판 삼아, 데이터 간의 풍부한 의미적 맥락을 반영하는 구조 설계에 깊은 흥미를 가지게 되었습니다. 향후 다양한 객체 간의 유기적인 관계를 다루는 딥러닝 기반 그래프 모델링 기법을 도입하여, 잠재적인 위험 요소를 사전에 스크리닝하거나 맞춤형 타겟팅을 예측하는 고도화된 모델링 역량을 갖추고자 합니다.
