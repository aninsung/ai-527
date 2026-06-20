# Chest X-ray Image Captioning using ResNet50 and BioBERT

## Project Overview

본 프로젝트는 Chest X-ray 영상을 입력받아 자동으로 의료 소견(Medical Findings)을 생성하는 의료 영상 캡셔닝(Image Captioning) 시스템을 구현하는 것을 목표로 한다.

이미지 특징 추출을 위해 ResNet50을 사용하고, 생성된 의료 보고서를 BioBERT를 이용하여 분석함으로써 질병 정보를 추출하고 의료 영상 해석을 지원한다.

---

## Motivation

흉부 X-ray는 폐렴(Pneumonia), 심장비대(Cardiomegaly), 흉막삼출(Pleural Effusion) 등 다양한 질환 진단에 사용되는 대표적인 의료 영상이다.

그러나 의료 영상 판독에는 전문 의료진의 많은 시간과 노력이 필요하며, 대량의 의료 데이터를 효율적으로 처리하기 위한 자동화 기술이 요구되고 있다.

본 프로젝트는 Deep Learning과 Natural Language Processing 기술을 결합하여 의료 영상으로부터 자동으로 설명 문장을 생성하고, 생성된 보고서를 기반으로 질병 정보를 추출하는 시스템을 구축한다.

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
 Disease Information
```

---

## Model Components

### 1. Image Encoder

- ResNet50
- Chest X-ray 이미지 특징 추출
- CNN 기반 Feature Map 생성

### 2. Report Generator

- Transformer Decoder
- 의료 보고서 자동 생성
- Findings 및 Impression 생성

### 3. Medical NLP

- BioBERT
- 생성된 보고서 분석
- 질병명(Entity) 추출
- 의료 개체 인식(NER)

---

## Dataset

### MIMIC-CXR

- 377,110 Chest X-ray Images
- 227,835 Radiology Reports
- 실제 임상 환경의 판독 보고서 제공

### IU X-Ray Dataset

- 7,470 Images
- 3,955 Reports
- 의료 영상 캡셔닝 연구에 널리 사용

---

## Technologies

- Python
- PyTorch
- ResNet50
- Transformer
- BioBERT
- NumPy
- Pandas
- Matplotlib

---

## Training Process

1. Chest X-ray 이미지 입력
2. ResNet50을 이용한 Feature Extraction
3. Transformer Decoder를 통한 Report Generation
4. Generated Report 생성
5. BioBERT를 이용한 Medical Text Analysis
6. 질병 정보 추출 및 결과 출력

---

## Evaluation Metrics

### Image Captioning

- BLEU
- ROUGE-L
- METEOR
- CIDEr

### Medical Report Evaluation

- Clinical Accuracy
- Disease Detection Accuracy
- Precision
- Recall
- F1-Score

---

## Expected Results

- Chest X-ray 기반 자동 의료 보고서 생성
- 의료진의 판독 업무 보조
- 의료 영상 분석 자동화
- 질병 정보 추출 및 임상 의사결정 지원

---

## Future Work

- Vision Transformer(ViT) 적용
- Attention Visualization
- BioGPT 및 ClinicalBERT 비교 실험
- Explainable AI(XAI) 기반 해석 가능성 향상
- Multi-modal Medical Foundation Model 연구

---

## References

- ResNet: Deep Residual Learning for Image Recognition
- BioBERT: A Pre-trained Biomedical Language Representation Model
- MIMIC-CXR Dataset
- IU X-Ray Dataset
