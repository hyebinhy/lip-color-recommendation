# 올리브영 립 제품 색상 분석 & 추천 시스템

> Development of a Personalized Lip Color Recommendation System: A Review and Color Similarity-Based Approach

## 프로젝트 소개

올리브영에서 판매되는 **1,529개 립 제품**의 색상을 이미지에서 자동 추출하고, PCCS 톤 체계로 분류한 뒤, **14,700건의 사용자 리뷰** 데이터를 활용한 협업 필터링 기반 맞춤형 립 제품 추천 시스템입니다.

기존 립 제품 추천이 단순 인기순이나 카테고리 기반인 것과 달리, **색상 유사도**와 **리뷰 평점(발색력, 지속력, 밀착력, 보습력)**을 결합하여 사용자 취향에 맞는 제품을 추천합니다.

## 시스템 파이프라인

```
1. 데이터 수집     올리브영 크롤링 → 립 제품 이미지 + 리뷰 수집
       ↓
2. 색상 추출      제품 이미지에서 RGB 색상 추출 (K-Means 클러스터링)
       ↓
3. 톤 분류       RGB → HSV 변환 → PCCS 톤 체계 분류 (명도/채도 기반)
       ↓
4. 리뷰 분석      발색력, 지속력, 밀착력, 보습력 평점 전처리
       ↓
5. 추천 모델      Matrix Factorization 기반 협업 필터링
       ↓
6. 최종 추천      색상 유사도(유클리드 거리) + 예측 평점 결합
```

## 주요 기능

### 1. 립 제품 크롤링
- Selenium을 활용한 올리브영 립 제품 정보 자동 수집
- 제품명, 가격, 제형(글로시/매트 등), 색상 이미지, 사용자 리뷰 수집

### 2. 색상 추출 및 분석
- 제품 이미지에서 K-Means 클러스터링으로 대표 RGB 색상 추출
- RGB, HSV 색상 공간에서의 3D/2D 시각화 (산점도, 색상환, 원뿔 모델)
- 명도(Lightness)와 채도(Saturation) 정량 분석

### 3. PCCS 톤 분류
- 추출된 색상을 PCCS(Practical Color Co-ordinate System) 톤 체계로 자동 분류
- 톤 카테고리: vivid, bright, strong, deep, light, soft, dull, dark, pale, light grayish, grayish, dark grayish
- 색상 계열: Pink, Red, Orange, Brown, Yellow, Purple, White

### 4. 리뷰 기반 추천 모델
- User-Item Matrix 구성 (사용자 x 제품 평점)
- Matrix Factorization(MF)으로 잠재 요인 학습
- 사용자별 평균 정규화 → Sigmoid 변환으로 예측 평점 산출
- 색상 유사도(유클리드 거리)와 결합한 최종 추천

## 데이터

| 데이터 | 설명 | 규모 |
|---|---|---|
| `OliveYoung_LIPLIST.csv` | 올리브영 립 제품 목록 | 1,529개 제품 |
| `extracted_colors.csv` | 제품별 추출 RGB 색상 | RGB, 비율 |
| `converted_colors.csv` | 색상 + 제형/가격/톤 통합 | HEX, 명도, 채도, 톤 |
| `전처리데이터/review.csv` | 사용자 리뷰 | 14,700건 |
| `review_table/user-item_table.csv` | User-Item 평점 매트릭스 | 발색/지속/밀착/보습 |

## 프로젝트 구조

```
├── notebooks/          # Jupyter 노트북 (분석 및 모델링 코드)
│   ├── oliveyoung.ipynb           # 올리브영 크롤링
│   ├── color space.ipynb          # 색상 공간 분석 (RGB/HSV 시각화)
│   ├── get RGB.ipynb              # RGB 색상 추출
│   ├── get_PCCS.ipynb             # PCCS 톤 추출
│   ├── 톤분류코드.ipynb              # 톤 분류 알고리즘
│   ├── Real_Classification.ipynb  # 색상 분류
│   ├── 명도,채도 확인.ipynb           # 명도/채도 분석
│   ├── MF-based CF.ipynb          # Matrix Factorization 추천 모델
│   ├── Latent Factor Model.ipynb  # 잠재 요인 모델
│   └── 캡스톤 최종.ipynb              # 최종 통합 코드
├── data/               # 데이터셋
│   ├── OliveYoung_LIPLIST.csv     # 립 제품 목록
│   ├── extracted_colors.csv       # 추출된 색상 데이터
│   ├── converted_colors.csv       # 변환된 색상 데이터 (통합)
│   ├── tone.csv                   # 톤 분류 결과
│   ├── 색상표_with_PCCS.csv        # PCCS 색상표
│   ├── review_table/              # 리뷰 기반 user-item 테이블
│   ├── 리뷰데이터/                  # 원본 리뷰 데이터
│   └── 전처리데이터/                 # 전처리된 데이터
├── images/             # 시각화 및 참고 이미지
│   ├── color_plot/                # 색상 분석 시각화
│   └── reference/                 # PCCS 기준 색상
└── docs/               # 발표 자료 및 보고서
```

## 기술 스택

| 분류 | 기술 |
|---|---|
| 언어 | Python |
| 데이터 수집 | Selenium, BeautifulSoup |
| 색상 분석 | OpenCV, scikit-image, K-Means Clustering |
| 시각화 | Matplotlib (3D scatter, polar plot, HSV cone) |
| 추천 모델 | Matrix Factorization, Collaborative Filtering, Scipy |
| 데이터 처리 | Pandas, NumPy |
| 환경 | Google Colab |
