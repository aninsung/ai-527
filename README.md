# 🩺 Biomedical Image Captioning with ResNet & BioBERT

> **ResNet(시각 인코더)과 BioBERT(언어 디코더)를 결합하여 의료 영상(Chest X-ray)을 분석하고 자동으로 의학적 소견(Findings & Impression)을 생성하는 멀티모달 이미지 캡셔닝 시스템입니다.**

본 프로젝트는 의료 영상 데이터의 시각적 특징을 추출하고, 생물의학 도메인에 특화된 언어 모델을 통해 실제 의료 현장에서 자문으로 활용할 수 있는 고품질의 텍스트 소견을 생성하는 것을 목표로 합니다.

---

## 🏗️ 시스템 아키텍처 (Model Architecture)

본 모델은 **Encoder-Decoder** 구조를 따르는 멀티모달 프레임워크입니다.

```text
[입력: 의료 이미지] ──> ResNet (Visual Encoder) ──> 시각 특징 벡터 (Visual Features)
                                     │
                                     ▼
[출력: 의학 소견] <── BioBERT (Language Decoder) <── Cross-Attention Fusion
```

### 1. Visual Encoder: ResNet

* **역할**: 입력된 Chest X-ray 이미지에서 병변의 위치, 음영, 형태 등 시각적 특징을 추출합니다.
* **특징**: ImageNet 및 의료 이미지 데이터로 사전 학습된 가중치를 활용하며, Global Average Pooling을 통해 고차원 특징 맵을 1차원 시각 특징 벡터로 변환합니다.

### 2. Language Decoder: BioBERT

* **역할**: 추출된 시각적 특징을 기반으로 자연스러운 생물의학 텍스트(소견)를 생성합니다.
* **특징**: PubMed, PMC 등의 대규모 의학 코퍼스로 사전 학습되어 `Pneumonia`, `Infiltration` 등 전문적인 의학 용어를 정확하게 이해하고 생성합니다.
* Cross-Attention 메커니즘을 통해 이미지 특징을 디코딩 과정에 반영합니다.

---

## 📊 데이터셋 구조 (Dataset Structure)

본 프로젝트는 이미지 데이터와 이에 매칭되는 의료 레포트 데이터를 활용합니다.

| 컬럼명 (Column) | 설명 (Description)                       |
| ------------ | -------------------------------------- |
| `filename`   | Chest X-ray 이미지 파일 경로                  |
| `projection` | 촬영 방향 (Frontal, Lateral 등)             |
| `findings`   | 이미지에 대한 방사선학적 세부 소견 (학습 Target Text)   |
| `impression` | 소견을 바탕으로 내린 최종 의학적 결론 (학습 Target Text) |

---

## 🚀 시작하기 (Quick Start)

### 1. 환경 설정 (Installation)

필요한 패키지를 설치합니다.

```bash
pip install torch torchvision transformers pandas matplotlib scikit-learn
```

### 2. 데이터 준비

데이터셋 파일과 이미지 폴더를 아래와 같은 구조로 배치합니다.

```text
.
├── data/
│   ├── images/
│   └── medical_data.csv
├── biobert.ipynb
└── README.md
```

### 3. 모델 학습 및 평가 (Training & Evaluation)

`biobert.ipynb` 노트북을 실행하여 모델을 학습시킵니다.

포함 내용:

* 데이터 로딩 및 전처리
* BioBERT 토큰화
* ResNet 특징 추출
* Visual Feature + Text Embedding 결합
* Loss 계산
* Epoch별 성능 평가

```python
N_EPOCHS = 10
BATCH_SIZE = 16
LEARNING_RATE = 5e-5
```

---

## 📈 학습 결과 (Results)

학습이 완료되면 Train Loss와 Test Loss의 수렴 과정을 그래프로 확인할 수 있습니다.

* Train & Test Loss over Epochs
* Cross-Entropy Loss 기반 최적화
* Epoch별 성능 추적
* 학습 진행 상황 디버깅 로그 출력

---

## 🛠️ 기술 스택 (Tech Stack)

### Framework

* PyTorch

### Computer Vision

* Torchvision
* ResNet

### Natural Language Processing

* Hugging Face Transformers
* BioBERT

### Data Analysis

* Pandas
* NumPy
* Scikit-learn

### Visualization

* Matplotlib

---

## 📚 프로젝트 목표

본 프로젝트의 목표는 의료 영상과 생물의학 언어 모델을 결합한 멀티모달 AI 시스템을 구축하여 의료 영상 분석 자동화 가능성을 탐구하는 것입니다.

### 주요 기능

* Chest X-ray 이미지 특징 추출
* 의료 영상 기반 자동 캡셔닝
* BioBERT 기반 의학 소견 생성
* 멀티모달 Encoder-Decoder 구조 구현
* 의료 AI 연구 및 교육 목적 활용

---

## 👨‍💻 Authors

Gachon University Computer Engineering

Biomedical Image Captioning Project
