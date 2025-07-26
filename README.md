# YOLO : 도로 주행 객체 탐지
- [2024년 자율주행 인공지능 알고리즘 개발 챌린지](https://challenge.gcontest.co.kr/template/m/frame/info1/16335)에 개인으로 참가해 진행한 프로젝트입니다.
- Object Detection의 핵심 원리를 이해한 후, YOLO 모델 학습과 직접 촬영한 도로 주행 영상에서 객체 탐지를 수행합니다.
- 가장 높은 모델 성능으로 [최우수상](https://graceful-cello-0d4.notion.site/2024-2347d8d98aa880b2ba62fd45ca0eda7c?source=copy_link)을 수상했습니다.

<Br>

## 배경
- 대회 기간 : <ins>2024. 7. 15. ~ 2024. 8. 19.</ins>
- 직접 모델을 개발하는 것에 흥미를 느껴 참가하게 됨
- [대회 규칙](https://challenge.gcontest.co.kr/template/m/frame/info2/16335)

<Br>

## YOLO 객체 탐지 모델
- YOLO (You Only Look Once)는 객체 감지(Object Detection)를 위한 딥러닝 모델로 이미지를 한 번만 보고도 객체의 위치와 종류를 동시에 파악한다.
- 즉, 여러 번의 처리 과정을 거치지 않고 한 번의 연산으로 객체 감지를 수행해 속도가 빠르다는 장점이 있다. <br>

  #### 1. 주요 특징
  - 실시간 객체 감지: YOLO는 이미지 전체를 한번에 처리하여 객체를 감지하기 때문에, 동영상이나 실시간으로 움직이는 물체를 감지해야 하는 경우에 유용함
  - 단일 신경망: 객체 감지 작업을 단일 신경망으로 처리하여 복잡한 계산을 줄이고 속도를 향상시킴
  - 빠른 처리 속도: 기존의 객체 감지 방식보다 훨씬 빠른 속도로 객체 감지가 가능함
  - 정확도: 속도뿐만 아니라 객체 감지 정확도도 높아서 실용적으로 사용됨 <br>

  #### 2. 동작 방식
  1. 입력 이미지를 그리드 셀로 나눔
  2. 각 그리드 셀은 여러 개의 Bounding Box(객체의 위치를 나타내는 사각형)를 예측함
  3. 각 바운딩 박스에 대한 객체 종류와 신뢰도 점수를 계산함
  4. 최종적으로 NMS(Non-Maximum Suppression)라는 과정을 통해 중복된 바운딩 박스를 제거하고 가장 정확한 예측 결과를 얻음 <br>

  #### 3. 사전 학습 모델
  - YOLO는 사전 학습 모델(pre-trained model)로 Ultralytics라는 회사에서 개발한 객체 탐지 모델임
  - [Ultralytics 공식 GitHub](https://github.com/ultralytics/ultralytics)에서 모델을 다운받고 몇가지 전처리 과정을 거치면 쉽게 나만의 객체 탐지 모델을 만들 수 있음
  - 객체 감지 외에도 분류(Classification), 이미지 세분화(Instance Semantic Segmentation), 포즈 추정(Pose Estimation) 등의 기능을 수행하는 모델을 배포하고 있음



- YOLO는 
- YOLO는 COCO8 데이터셋을 사전 학
- YOLO 객체 탐지 모델은 직사각형으로 탐지한 객체의 위치를 나타냄 (해당 직사각형을 Bounding Box, 약자로 BBox라고 함)
- YOLO 모델을 학습시키기 위해 Ultralytics GitHub 홈페이지에서 모델을 다운받고아래와 같은 데이터셋 구조를 만들고 yaml 파일을 생성해야 함 <br><br>
<p align="center">
[데이터셋 구조]
</p>
<p align="center">
<img width="135" height="234" alt="image" src="https://github.com/user-attachments/assets/aef1c6c0-2445-4534-bfc7-e16f65fd6178" />
</p>
<p align="center"> <br>
[yaml 파일 예시]
</p>
<p align="center">
<img width="639" height="260" alt="image" src="https://github.com/user-attachments/assets/0d23e3a3-f9fc-47ba-aac2-3215e83ce84b" />
</p>

## 사용 데이터
- 주최측에서 제공된 ['한국교통안전공단 자율주행 공개 데이터셋'](https://drive.google.com/file/d/1ee4kSO4iqnhErrxRnvZ2qTlbe-Iazsov/view?usp=sharing)(40.9GB)
- 1920x1200 크기 도로 주행 이미지 10만 장과 객체 10종의 위치 정보 파일(.json) 10만 개
  - 학습 데이터셋 : 80,000 images 
  - 검증 데이터셋 : 10,000 images 
  - 테스트 데이터셋 : 10,000 images

- 객체 위치 정보 파일(.json) 속성

  <img width="590" height="182" alt="Image" src="https://github.com/user-attachments/assets/69e214f6-9391-41f0-a44a-8d6c3b80aba1" />

<br>

## YOLO 선택 배경
- YOLO는 You Only Look Once의 약자로 이미지를 한 번만 보고도 예측을 수행하며 객체 검출 성능이 좋은 모델로 알려짐
- 사용자 친화적인 UI를 제공하며 간단한 코드 몇 줄 만으로 모델 학습 및 검증 결과를 알 수 있음

<br>

## 개발 과정
### 1. 객체 위치 정보 정규화
- 해당 과정은 YOLO 객체 탐지 모델을 학습시키기 위해 필수로 거쳐야 하는 과정임
- 객체 위치 정보 파일(.json) 구조 예시
<p align="center">
<img width="333" height="432" alt="Image" src="https://github.com/user-attachments/assets/c8b47ed1-5f2b-4110-9e6b-4ad034b28de7" />
</p>

<br>

 #### 막간 지식
 - YOLO 객체 탐지 모델은 직사각형으로 탐지한 객체의 위치를 나타냄
 - 해당 직사각형을 Bounding Box, 약자로 BBox라고 함
 - 모델이 객체의 특성을 학습하고 새로운 이미지에서 객체 탐지를 수행하기 위해 모델에게 객체 위치 정보를 알려주어야 하는데
 - YOLO의 경우 아래와 같은 내용이 포함된 파일의 경로를 yaml 파일에 지정해서 모델이 객체의 특성을 학습할 수 있도록 함
<br>
<br>
<p align="center">
🚀 YOLO 형식 객체 위치 정보 🚀
</p>
<p align="center">
[객체 라벨, 객체 중심 좌표(x,y), 객체 가로길이(w), 객체 세로길이(h)]
</p>
<p align="center">
객체 라벨은 0 부터 시작하는 정수이며 위치 정보는 0 ~ 1 사이의 값을 갖음
</p>
<p align="center">
파일은 txt 파일 형식으로 이미지 파일명과 동일함 (파일 확장자 제외)
</p>
<p align="center">
편의를 위해 해당 txt 파일을 yolo format txt 파일이라 하겠음
</p>
<br>
<p align="center">
우리가 사용하는 데이터에서 객체 위치 정보는 Bounding Box의 좌측 상단 좌표(x_min, y_min), 우측 하단 좌표(x_max, y_max)로 제공됨
</p>
<p align="center">
x_min, x_max는 0 ~ 1920의 값을 갖고 y_min, y_max는 0 ~ 1200의 값을 갖음
</p>
<p align="center">
(해당 정보는 labels 폴더 json 파일의 [Annotation][data] 변수에 들어있음)
</p>
<p align="center">
해당 좌표를 활용해서 객체의 중심 좌표, 가로 길이, 그리고 세로 길이를 구하고
</p>
<p align="center">
원본 이미지 크기(image_width, image_height)로 나눠서 yolo format txt 파일을 생성함
</p>
<p align="center">
(해당 과정은 <ins>객체 위치 정보 정규화.ipynb</ins> 파일에서 확인 가능)
</p>
<br>
<br>

### labels 폴더의 json 파일에서 추출한 정보
- 이미지 파일명
- 원본 이미지 가로길이 (image_width)
- 원본 이미지 세로길이 (image_height)
- 객체명
- 객체 위치 정보 (x_min, y_min, x_max, y_max)

<br>

#### 객체 중심 좌표, 가로 길이, 세로 길이 구하기
- x = (x_min + x_max) / 2
- y = (y_min + y_max) / 2
- w = x_max - x_min
- h = y_max - y_min
- x와 w는 0 ~ 1920, y와 h는 0 ~ 1200 사이의 값

<br>

#### 정규화 식
- yolo format x = x / image_width
- yolo format y = y / image_height
- yolo format w = w / image_width
- yolo format h = h / image_height
- yolo format x, y, w, h는 0 ~ 1 사이의 값

<br>

### 객체 정수 라벨
| class | label |
|:------|:--------|
| car | 0 |
| bus | 1 |
| truck | 2 |
| special vehicle | 3 |
| motorcycle | 4 |
| bicycle | 5 |
| personal mobility | 6 |
| person | 7 |
| Traffic_light | 8 |
| Traffic_sign | 9 |

<br>
<br>

- 변환 결과 예시
<p align="center">
<img width="247" height="130" alt="1" src="https://github.com/user-attachments/assets/e4e16ba8-8d67-4eb5-8e54-528da78cacb0" />
</p>

<br>
<br>
<br>

### 2. Base 모델 학습

| Model | epoch | batch | mAP@50 | 학습 시간 | 모델 구조 | 파일명 |                                       
|:-----:|:-----:|:-----:|:------:|:---------:|:---------:|:------:|
| yolov8n.pt | 100 | 64 | 0.71 | 21.67 hours | 225 layers, 3,012,798 parameters | 8n_100.pt |
| yolov8s.pt | 100 | 64 | 0.821 | 22.23 hours | 225 layers, 11,139,470 parameters | 8s_100.pt |
| yolov8m.pt | 100 | 64 | 0.866 | 23.34 hours | 295 layers, 25,862,110 parameters | 8m_100.pt |
| yolov8l.pt | 100 | 64 | 0.888 | 24.17 hours | 365 layers, 43,637,550 parameters | 8l_100.pt |
| yolov8x.pt | 100 | 64 | 0.901 | 28.61 hours | 365 layers, 68,162,238 parameters | 8x_100.pt |

<br>
<br>
<br>

### 3. 최종 모델 학습
| Model | epoch | batch | mAP@50 | 학습 시간 | 모델 구조 | 파일명 |                                       
|:-----:|:-----:|:-----:|:------:|:---------:|:---------:|:------:|
| yolov8x.pt | 620 | 64 | 0.933 | 약 7일 21시간 | 365 layers, 68,162,238 parameters | 8x_620.pt |

<img width="600" height="300" alt="results" src="https://github.com/user-attachments/assets/b93ab859-a1f2-426f-9c90-45c0ac75b1bf" />

<br>
<br>
<br>

### 4. 시연 영상

- [test dataset](https://github.com/user-attachments/assets/715ef921-bc30-4d1c-8d89-b6caf0dff56a)

- [daytime](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [night](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

