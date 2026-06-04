# 💊 약물 공동처방 네트워크 분석 (Analysis of Drug Co-prescription Network)

<!-- 미리캔버스/캔바 등을 활용해 제작한 미니멀하고 기하학적인 느낌의 커버 이미지를 여기에 삽입하세요 -->
<div align="center">
  <img src="배너이미지URL" alt="Project Banner" width="800"/>
</div>

<br/>

<div align="center">
  <!-- State Blue(#4B5EFC) 컬러를 적용한 배지 -->
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/NetworkX-4B5EFC?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Gephi-4B5EFC?style=for-the-badge&logo=databricks&logoColor=white"/>
</div>

## 📌 1. 프로젝트 개요 (Overview)
* **배경:** COVID-19 장기화로 인한 우울 위험군 및 항우울제 처방 건수의 급증. 기존 연구들은 단일 약품 처방 패턴 분석에 머물러 있어, 약물 간의 '공동 처방' 패턴과 그에 따른 상호작용(DDI)을 파악하기 어려움.
* **목표:** 
  1. 2017년~2021년 한국 환자들의 **항우울제 공동처방 네트워크 구축 및 시계열 변화(COVID-19 전후) 분석**
  2. 연령대별 우울증 유무에 따른 **만성질환 네트워크(Community Structure) 대조 분석**

## 📊 2. 데이터셋 및 전처리 (Data & Preprocessing)
* **데이터 소스:** 국민건강보험공단 의약품 처방정보 (5개년, 연도별 무작위 100만 명 샘플 데이터)
* **전처리 핵심:**
  * 상이한 주성분 코드(9자리)를 체계적인 분류를 위해 세계보건기구(WHO) 기준 **ATC 코드**로 일괄 매핑 (`mapping.csv` 구축)
  * 분석 타겟팅을 위해 항우울제(N06A) 및 주요 만성질환(8종) 관련 ATC 코드 추출 및 엣지(동시 처방) 구성

## 🔬 3. 핵심 분석 방법론 (Methodology)
* **거시적 네트워크 분석 (Macroscopic Analysis):** Density, Mean Degree, Transitivity 측정을 통한 네트워크 연결성 파악
* **중심성 분석 (Centrality Analysis):** Degree, Eigenvector, Betweenness Centrality를 비교하여 네트워크 내 가교 역할을 하는 핵심 약물(Bridge Drug) 탐색
* **확률적 블록 모델링 (Stochastic Block Modeling, SBM):** 질환 네트워크 내의 군집 구조(Community Structure)를 통계적으로 탐지하여, 병용 처방 빈도가 높은 만성질환 블록 식별

## 💡 4. 주요 분석 결과 (Key Findings)
1. **네트워크 밀도 증가:** 코로나 전후 기간 동안 항우울제 공동처방 엣지 수 및 전이성(Transitivity)이 꾸준히 우상향하며, 처방 네트워크의 연결성이 강화됨.
2. **핵심 중개 약물의 변화:** 기존 가교 역할을 하던 '플루복사민'의 중심성이 점차 하락하고, '티아넵틴'이 서로 다른 작용 기전 그룹을 이어주는 새로운 중심 약물로 부상함.
3. **고령층 우울증과 치매의 연관성:** 65세 이상 고령층 우울증 환자의 만성질환 네트워크에서 '치매 관련 약물'의 Degree Centrality가 압도적으로 높게 나타남.
4. **만성질환 모듈성(Modularity) 감소:** 연령대가 높아질수록, 특히 우울증 환자군에서 네트워크의 Modularity 지표가 크게 감소함. 이는 고령층 우울증 환자가 복합 만성질환에 더 쉽게 노출되며, 약물 간 커뮤니티 경계가 허물어짐을 시사함.

## 🚀 5. 프로젝트 한계 및 발전 방향 (Limitations & Future Work)
* **데이터 한계 극복:** 현재 분석은 처방 내역을 곧 해당 질환의 발병으로 가정함. 향후 실제 환자의 진단 코드(ICD) 데이터가 확보된다면 더 정교한 분석이 가능함.
* **방향성 네트워크 및 이질적 정보 네트워크(HIN)로의 확장:** 본 프로젝트는 방향성이 없는(Undirected) 약물-약물 네트워크에 국한되었으나, 향후 환자-질병-약물을 모두 포함하는 다중 노드 구조의 **이질적 정보 네트워크(Heterogeneous Information Network, HIN)**로 모델링하고, **GNN(Graph Neural Networks)**을 활용한 약물 추천 시스템이나 이상 처방 탐지 알고리즘으로 발전시킬 수 있음.
