#CodeIT AI4 2팀 초급 프로젝트
# 💊 Pill Detection with YOLOv8

본 프로젝트는 경구 약제 이미지를 활용하여 **객체 인식(Object Detection)** 모델을 개발 및 성능 향상을 목표로 합니다.  
데이터 분석(EDA) 진행 후 YOLOv8을 베이스라인 모델로 설정하고, 수도 라벨링과 다양한 2차 모델학습을 통한 성능 향상 전략을 적용하였습니다.  

---

## 📌 프로젝트 개요
- **Task:** 경구 약제 객체 인식 (Object Detection)  
- **모델:**
  - YOLOv8 (Ultralytics)
  - Fast R CNN
- **데이터 출처:** Kaggle 제공 데이터셋 (ai04-level1-project)  
- **환경:** Google Colab + PyTorch  

---

## 🔍 데이터 분석 (EDA)
EDA 과정에서 확인한 주요 사항은 다음과 같습니다:
- 데이터셋 클래스 및 이미지 분포 확인  
- 일부 클래스 불균형 존재  
- 라벨 누락 및 오류 발견  
- 전처리 및 증강 전략 필요성 도출  

---

## 📂 데이터 준비
- Google Drive 및 Kaggle 연동  
- 압축 해제 후 프로젝트 디렉토리 구성  
- YOLO 학습을 위한 **YAML 파일 자동 생성**  

---

## 📌 베이스라인 모델
- **모델:** YOLOv8n (pretrained weights: COCO)  
- **학습 파라미터**
  - Epochs: 50  
  - Batch size: 16  
  - Optimizer: AdamW  
- **평가 지표:** mAP@0.5-095 , kaggle 평가 지표  

### 📊 Baseline 성능
- mAP@0.5-0.95: 약 0.849
- kaggle 지표 : 0.97414

---

## 🚀 성능 향상 전략
EDA와 베이스라인을 기반으로, 이후 단계에서는 다음과 같은 방법으로 성능을 개선했습니다:

1. **데이터 라벨 보정** (누락/오류 라벨 수정)
2. **수도 라벨링(pseudo labeling)**
3. **다양한 2차 학습 모델 사용**  

---

## 📌 다양한 모델 학습 결과
1. yolov8s -> yolov8n
   - 큰 모델로 학습 후 작은 모델로 학습
   - 성능이 더 떨어짐 0.97715 -> 0.78027
   - 큰 모델로 학습 한 데이터 셋과 수도라벨링을 진행한 데이터 셋의 간극이 커 데이터 예측이 제대로 진행되지 않음
  예측 예시 :
  <img width="1170" height="715" alt="1216_comparison" src="https://github.com/user-attachments/assets/ae9394c6-02a1-4c66-9f2a-5399c4a73a7b" />

2. 앙상블 라벨링
   - 여러 수도라벨링 방법 중 하나로 다양한 모델의 결과를 통해 교차검증을 거쳐 수도라벨리을 진행
   - 위 수도라벨링과 동일하게 성능이 떨어짐 0.97715 -> 0.9676
  예측 예시 :
  <img width="1774" height="378" alt="스크린샷 2025-09-23 오전 10 48 11" src="https://github.com/user-attachments/assets/9cc78db4-b7ba-4484-9849-2d05b56ef68e" />

  
3. Fast R CNN
   - yolov8s로 학습 한 이후 수도라벨링을 진행하고 2차 학습 모델로 Fast R CNN 모델 사용
   - 해당 모델 역시 성능이 저하됨
---

## 🏆 최종 결과
- 최종 모델: YOLOv8s (custom dataset)  
- Epoch: 100  
- mAP@0.5: **0.984**  

예측 예시:  
<img width="1308" height="788" alt="1_comparison" src="https://github.com/user-attachments/assets/c9c8101a-518b-42d8-b592-655461d34ffb" />

---
