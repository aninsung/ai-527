# Chest X-ray Image Captioning with ResNet50, Ramen, and BioBERT

## Project Overview

본 프로젝트는 Chest X-ray 영상을 입력받아 의료 소견(Medical Findings)을 자동 생성하고, 생성된 보고서를 분석하여 질병 정보를 추출하는 의료 영상 캡셔닝 시스템이다.

특히 최근 제안된 Ramen(Robust Test-Time Adaptation with Active Sample Selection)을 적용하여 병원별 장비 차이, 촬영 환경 차이, 데이터 분포 변화(Domain Shift)에 강인한 의료 영상 분석 모델을 구축하는 것을 목표로 한다.

---

## Motivation

의료 영상 데이터는 병원마다 다음과 같은 차이를 가진다.

- 촬영 장비 차이
- 영상 해상도 차이
- 환자 분포 차이
- 노이즈 및 영상 품질 차이

이러한 Domain Shift는 모델 성능 저하를 유발한다.

본 프로젝트는 Ramen 기반 Test-Time Adaptation을 통해 새로운 환경에서도 안정적인 성능을 유지할 수 있는 Chest X-ray Captioning 시스템을 개발한다.

---

## System Architecture

```text
Chest X-ray Image
        │
        ▼
     ResNet50
(Image Feature Extraction)
        │
        ▼
      Ramen
(Test-Time Adaptation)
        │
        ▼
 Transformer Decoder
(Report Generation)
        │
        ▼
 Generated Findings
        │
        ▼
     BioBERT
(Medical Text Analysis)
        │
        ▼
 Disease Prediction
```

---

## Model Components

### 1. ResNet50 Encoder

- Chest X-ray 특징 추출
- CNN 기반 Feature Representation 생성

### 2. Ramen (Test-Time Adaptation)

- Active Sample Selection
- Domain Consistency 유지
- Prediction Balance 적용
- Mixed-Domain 환경 적응
- Test 단계에서 모델 자동 적응

주요 역할

- 병원 간 데이터 분포 차이 완화
- 새로운 환경에서 성능 유지
- 강건한 Feature Representation 생성

### 3. Transformer Decoder

- 의료 보고서 생성
- Findings 생성
- Impression 생성

예시

```text
Mild cardiomegaly is noted.
No pleural effusion is observed.
```

### 4. BioBERT

- 생성된 의료 보고서 분석
- 질병 개체 추출
- Medical NLP 수행

---

## Dataset

### MIMIC-CXR

- 377,110 Images
- 227,835 Studies
- 실제 임상 판독 보고서 제공

### IU X-Ray Dataset

- 7,470 Images
- 3,955 Reports

---

## Technologies

- Python
- PyTorch
- ResNet50
- Transformer Decoder
- BioBERT
- Ramen
- NumPy
- Pandas
- Matplotlib

---

## Training Pipeline

### Stage 1

Chest X-ray Image Encoder 학습

```text
Image
↓
ResNet50
↓
Feature Vector
```

### Stage 2

Medical Report Generation 학습

```text
Feature Vector
↓
Transformer Decoder
↓
Report
```

### Stage 3

BioBERT 기반 의료 텍스트 분석

```text
Report
↓
BioBERT
↓
Disease Extraction
```

### Stage 4

Test-Time Adaptation

```text
New Hospital Data
↓
Ramen
↓
Model Adaptation
↓
Robust Caption Generation
```

---

## Evaluation Metrics

### Captioning

- BLEU-1
- BLEU-2
- BLEU-3
- BLEU-4
- METEOR
- ROUGE-L
- CIDEr

### Clinical Evaluation

- Precision
- Recall
- F1-score
- Disease Detection Accuracy

### Robustness Evaluation

- Domain Shift Accuracy
- Mixed-Domain Accuracy
- Adaptation Gain

---

## Expected Outcomes

- 자동 의료 보고서 생성
- 질병 정보 자동 추출
- 병원 간 Domain Shift 대응
- 강건한 의료 영상 분석 시스템 구축
- 의료진 의사결정 지원

---

## References

- ResNet: Deep Residual Learning for Image Recognition
- BioBERT: Biomedical Language Representation Model
- Ramen: Robust Test-Time Adaptation of Vision-Language Models with Active Sample Selection
- MIMIC-CXR Dataset
- IU X-Ray Dataset
