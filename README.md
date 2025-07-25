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

## 사용 데이터
- 주최측에서 제공된 ['한국교통안전공단 자율주행 공개 데이터셋'](https://drive.google.com/file/d/1ee4kSO4iqnhErrxRnvZ2qTlbe-Iazsov/view?usp=sharing)(40.9GB)
- 1920x1200 크기 도로 주행 이미지 10만 장과 객체 10종의 위치 정보 파일(.json) 10만 개
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
- 해당 과정은 YOLO 객체 탐지 모델을 학습시키기 위해 필수로 거쳐야 하는 과정임
- 객체 위치 정보 파일(.json) 구조 예시
<p align="center">
<img width="333" height="432" alt="Image" src="https://github.com/user-attachments/assets/c8b47ed1-5f2b-4110-9e6b-4ad034b28de7" />
</p>

<br>

 #### 막간 지식
 - YOLO 객체 탐지 모델은 직사각형으로 탐지한 객체의 위치를 나타냄
 - 모델이 객체의 특성을 학습하고 새로운 이미지에서 객체 탐지를 수행하기 위해 모델에게 객체 위치 정보를 알려주어야 하는데
 - YOLO의 경우 아래와 같은 내용이 포함된 폴더 경로를 yaml 파일에 지정하여 모델이 객체의 특성을 학습할 수 있도록 함
<br>
<p align="center">
**YOLO 형식 객체 위치 정보**
</p>
- [객체 라벨, 객체 중심 좌표(x,y), 객체 가로길이(w), 객체 세로길이(h)]
- 객체 라벨은 0 부터 시작하는 정수이며 위치 정보는 0 ~ 1 사이의 값을 갖음
- 파일은 txt 파일 형식으로 이미지 파일명과 동일함 (파일 확장자 제외)
- 편의를 위해 해당 txt 파일을 yolo format txt 파일이라 하겠음

<br>
<br>

- 변환 결과 예시
<p align="center">
<img width="247" height="130" alt="1" src="https://github.com/user-attachments/assets/e4e16ba8-8d67-4eb5-8e54-528da78cacb0" />
</p>

<br>
<br>

### 2. Base 모델 학습
<p align="center">
<img width="722" height="155" alt="image (2)" src="https://github.com/user-attachments/assets/fbc7bbc1-ffde-4628-a7eb-a4c1463476a4" />
</p>


<br>
<br>

### 3. 최종 모델 학습
<p align="center">
<img width="724" height="71" alt="image" src="https://github.com/user-attachments/assets/92f9c6e6-7bb9-4d52-ab29-cffcf208a011" />
</p>


<p align="center">
<img width="600" height="300" alt="results" src="https://github.com/user-attachments/assets/b93ab859-a1f2-426f-9c90-45c0ac75b1bf" />
</p>


<br>
<br>

### 4. 시연 영상

- [test dataset](https://github.com/user-attachments/assets/715ef921-bc30-4d1c-8d89-b6caf0dff56a)

- [daytime](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [night](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

