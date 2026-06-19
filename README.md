## 2024 2nd season: resnet 논문 리뷰
## 2024~2025 winter season task: image captioning(이미지를 text로 생성) 구현
### model: biobert(text) +resnet(image)


```markdown
# 🩺 Biomedical Image Captioning with ResNet & BioBERT

> **ResNet(시각 인코더)과 BioBERT(언어 디코더)를 결합하여 의료 영상(Chest X-ray)을 분석하고 자동으로 의학적 소견(Findings & Impression)을 생성하는 멀티모달 이미지 캡셔닝 시스템입니다.**

본 프로젝트는 의료 영상 데이터의 시각적 특징을 추출하고, 생물의학 도메인에 특화된 언어 모델을 통해 실제 의료 현장에서 자문으로 활용할 수 있는 고품질의 텍스트 소견을 생성하는 것을 목표로 합니다.

---

## 🏗️ 시스템 아키텍처 (Model Architecture)

본 모델은 **Encoder-Decoder** 구조를 따르는 멀티모달 프레임워크입니다.


```

[입력: 의료 이미지] ──> ResNet (Visual Encoder) ──> 시각 특징 벡터 (Visual Features)
│
▼
[출력: 의학 소견]   <── BioBERT (Language Decoder) <── [Cross-Attention Fusion]

```

### 1. Visual Encoder: ResNet
* **역할**: 입력된 Chest X-ray 이미지에서 병변의 위치, 음영, 형태 등 시각적 특징을 추출합니다.
* **특징**: ImageNet 및 의료 이미지 데이터로 사전 학습된 중량(Weight)을 활용하며, Global Average Pooling을 통해 고차원 특징 맵을 1차원 시각 특징 벡터로 변환합니다.

### 2. Language Decoder: BioBERT
* **역할**: 추출된 시각적 특징을 기반으로 자연스러운 생물의학 텍스트(소견)를 생성합니다.
* **특징**: PubMed, PMC 등의 대규모 의학 코퍼스로 사전 학습되어 `Pneumonia(폐렴)`, `Infiltration(침윤)` 등 전문적인 의학 용어 맥락을 정확하게 이해하고 생성합니다. Cross-Attention 메커니즘을 통해 이미지 특징을 디코딩 과정에 반영합니다.

---

## 📊 데이터셋 구조 (Dataset Structure)

본 프로젝트는 이미지 데이터와 이에 매칭되는 의료 레포트 데이터를 활용합니다.

| 컬럼명 (Column) | 설명 (Description) |
| :--- | :--- |
| `filename` | Chest X-ray 이미지 파일 경로 |
| `projection` | 촬영 방향 (e.g., Frontal, Lateral) |
| `findings` | 이미지에 대한 방사선학적 세부 소견 (학습 Target text) |
| `impression` | 소견을 바탕으로 내린 최종 의학적 결론 (학습 Target text) |

---

## 🚀 시작하기 (Quick Start)

### 1. 환경 설정 (Installation)
필요한 패키지를 설치합니다.
```bash
pip install torch torchvision transformers pandas matplotlib scikit-learn

```

### 2. 데이터 준비

데이터셋 파일과 이미지 폴더를 아래와 같은 구조로 배치합니다.

```
.
├── data/
│   ├── images/          # X-ray 이미지 파일들
│   └── medical_data.csv # uid, filename, findings 등이 포함된 CSV
├── biobert.ipynb        # 메인 훈련 및 평가 스크립트
└── README.md

```

### 3. 모델 학습 및 평가 (Training & Evaluation)

`biobert.ipynb` 노트북을 실행하여 모델을 학습시킵니다. 데이터 로딩, 토큰화, ResNet+BioBERT 임베딩 결합, Loss 계산 및 에폭별 학습 그래프 출력이 포함되어 있습니다.

```python
# 노트북 내부 주요 파라미터 예시
N_EPOCHS = 10
BATCH_SIZE = 16
LEARNING_RATE = 5e-5

```

---

## 📈 학습 결과 (Results)

학습이 완료되면 Train Loss와 Test Loss의 수렴 경향을 확인할 수 있는 그래프가 시각화됩니다.

* **Train & Test Loss over Epochs**
* 크로스 엔트로피 손실 함수(Cross-Entropy Loss)를 사용하여 생성된 토큰과 실제 소견 간의 오차를 최소화합니다.
* 학습 진행 상황은 10개 샘플마다 디버깅 로그로 출력됩니다.



---

## 🛠️ 기술 스택 (Tech Stack)

* **Framework**: PyTorch
* **Computer Vision**: Torchvision (ResNet)
* **NLP**: Hugging Face Transformers (BioBERT)
* **Data Analysis**: Pandas, NumPy, Scikit-learn
* **Visualization**: Matplotlib

```

```
