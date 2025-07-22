# YOLO : 도로 주행 객체 탐지
- [2024년 자율주행 인공지능 알고리즘 개발 챌린지](https://challenge.gcontest.co.kr/template/m/frame/info1/16335)에 개인으로 참가해 진행한 프로젝트입니다.
- Object Detection의 핵심 원리를 이해한 후, YOLO 모델 학습과 직접 촬영한 도로 주행 영상에서 객체 탐지를 수행합니다.
- 가장 높은 모델 성능으로 [최우수상](https://graceful-cello-0d4.notion.site/2024-2347d8d98aa880b2ba62fd45ca0eda7c?source=copy_link)을 수상했습니다.

<Br>

## 배경
- 직접 모델을 개발하는 것에 흥미를 느껴 참가하게 됨
- [대회 규칙](https://challenge.gcontest.co.kr/template/m/frame/info2/16335)

<Br>

## 사용 데이터
- 주최측에서 제공된 한국교통안전공단 ['자율주행 공개데이터셋'](https://challenge.gcontest.co.kr/template/m/frame/downloadlist/16335?q=1368)(40.9GB)
- 1920x1200 크기 도로 주행 이미지 10만장과 객체 10종의 위치 정보 파일(.json) 10만개
  - 학습 데이터 세트 : 80,000 images 
  - 검증 데이터 세트 : 10,000 images 
  - 테스트 데이터 세트 : 10,000 images

- 객체 위치 정보 파일(.json) 속성

  <img width="590" height="182" alt="Image" src="https://github.com/user-attachments/assets/69e214f6-9391-41f0-a44a-8d6c3b80aba1" />

<br>

## YOLO 선택 배경
- YOLO는 You Only Look Once의 약자로 이미지를 한 번만 보고도 예측을 수행하며 객체 검출 성능이 좋은 모델로 알려짐
- 사용자 친화적인 UI를 제공하며 간단한 코드 몇 줄 만으로 모델 학습 및 검증 결과를 알 수 있음

<br>

## 개발 과정
### 1. 객체 위치 정보 정규화
- YOLO 모델 학습을 위해 객체 위치 정보를 0 ~ 1 사이의 값으로 변환하는 과정을 진행
- 객체 위치 정보 파일(.json) 구조 예시
<img width="333" height="432" alt="Image" src="https://github.com/user-attachments/assets/c8b47ed1-5f2b-4110-9e6b-4ad034b28de7" />

<br>
<br>

- 변환 결과 예시
<img width="247" height="130" alt="1" src="https://github.com/user-attachments/assets/e4e16ba8-8d67-4eb5-8e54-528da78cacb0" />

<br>
<br>

### 2. Base 모델 학습
<img width="722" height="155" alt="image (2)" src="https://github.com/user-attachments/assets/fbc7bbc1-ffde-4628-a7eb-a4c1463476a4" />


<br>
<br>

### 3. 최종 모델 학습
<img width="724" height="71" alt="image" src="https://github.com/user-attachments/assets/92f9c6e6-7bb9-4d52-ab29-cffcf208a011" />


<img width="1200" height="600" alt="results" src="https://github.com/user-attachments/assets/b93ab859-a1f2-426f-9c90-45c0ac75b1bf" />

<br>
<br>

### 4. 시연 영상
- [test dataset](https://github.com/user-attachments/assets/715ef921-bc30-4d1c-8d89-b6caf0dff56a)

- [daytime](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [night](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

