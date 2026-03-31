# 올리브영 립 제품 색상 분석 & 추천 시스템

2024 인공지능학과 캡스톤 디자인 프로젝트

## 프로젝트 소개

올리브영 립 제품의 색상을 추출하고 PCCS 톤 체계로 분류한 뒤, 사용자 리뷰 기반 협업 필터링(Collaborative Filtering)을 활용한 립 제품 추천 시스템입니다.

## 주요 기능

- **립 제품 크롤링**: 올리브영 사이트에서 립 제품 정보 수집
- **색상 추출 및 분석**: 제품 이미지에서 RGB 색상 추출, 명도/채도 분석
- **PCCS 톤 분류**: 추출된 색상을 PCCS 톤 체계(Pink, Red, Orange, Brown 등)로 분류
- **리뷰 기반 추천**: Matrix Factorization 기반 협업 필터링 추천 모델

## 프로젝트 구조

```
├── notebooks/          # Jupyter 노트북 (분석 및 모델링 코드)
│   ├── oliveyoung.ipynb           # 올리브영 크롤링
│   ├── color space.ipynb          # 색상 공간 분석
│   ├── get RGB.ipynb              # RGB 색상 추출
│   ├── get_PCCS.ipynb             # PCCS 톤 추출
│   ├── 톤분류코드.ipynb              # 톤 분류
│   ├── Real_Classification.ipynb  # 색상 분류
│   ├── 명도,채도 확인.ipynb           # 명도/채도 분석
│   ├── MF-based CF.ipynb          # Matrix Factorization 추천 모델
│   ├── Latent Factor Model.ipynb  # 잠재 요인 모델
│   └── 캡스톤 최종.ipynb              # 최종 통합 코드
├── data/               # 데이터셋
│   ├── OliveYoung_LIPLIST.csv     # 립 제품 목록
│   ├── extracted_colors.csv       # 추출된 색상 데이터
│   ├── converted_colors.csv       # 변환된 색상 데이터
│   ├── tone.csv                   # 톤 분류 결과
│   ├── 색상표_with_PCCS.csv        # PCCS 색상표
│   ├── review_table/              # 리뷰 기반 user-item 테이블
│   ├── 리뷰데이터/                  # 원본 리뷰 데이터
│   └── 전처리데이터/                 # 전처리된 데이터
├── images/             # 시각화 및 참고 이미지
│   ├── color_plot/                # 색상 분석 시각화
│   └── reference/                 # PCCS 기준 색상
└── docs/               # 발표 자료 및 보고서
    ├── 인공지능학과 캡스톤 최종 발표.pptx
    ├── 인공지능학과 캡스톤 최종 보고서.pdf
    ├── 캡스톤디자인포스터.pdf
    └── 캡스톤 최종발표 대본.pdf
```

## 기술 스택

- **언어**: Python
- **데이터 수집**: Selenium, BeautifulSoup
- **색상 분석**: OpenCV, scikit-image
- **추천 모델**: Matrix Factorization, Collaborative Filtering
- **환경**: Google Colab
