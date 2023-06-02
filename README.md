# 사람얼굴인식

![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)

이미지에서 사람 얼굴을 추출 후 추출한 이미지를 변형 시키는 프로젝트 입니다.

# 목차

- 소개
  - 프로젝트 개요
  - 목적과 목표
  - 기술 스택 및 환경
- 설치가이드
  - 설치방법
  - 설정 및 구성
- 사용법
  - 프로젝트 실행 방법
  - 주요 기능 
- 라이선스
  - 프로젝트에 대한 라이선스 정보

# 소개

## 프로젝트 개요

대학교 과제로 주어진 프로젝트였으며 주제는 자유였습니다.

당시 코로나로 인해 마스크 착용이 필수였음 이에 사용자의 마스크 착용에 대한 얼굴 인식 기술이 발달됨에 따라

얼굴 인식 기술에 대해 흥미가 생겨 문서를 찾아 본 후 본 프로젝트를 시작 하였습니다.

## 목적과 목표

이미지 안에 사람 얼굴을 추출 후 추출 한 이미지를 변경 및 적용 시킨다.


## 기술 스택 및 환경

기술 스택: python

환경: jupyter notebook && google colab

# 설치 가이드

## 설치방법

[파이썬](https://www.python.org/) 설치

[주피터노트북](https://jupyter.org/) 설치

## 설정 및 구성

구글 코랩을 사용해 이미지 업로드

shape_predictor_68_face_landmarks 모델 사용


# 사용법

## 프로젝트 실행 방법

파이썬 환경변수 설정 후 주피터 노트북으로 해당 코드 실행

## 주요 기능

코랩에 업로드 된 이미지 파일 불러오는 코드

```
# 필요한 파일들 읽음
faceDetector = dlib.get_frontal_face_detector()
landmarkDetector = dlib.shape_predictor("data/models/shape_predictor_68_face_landmarks.dat")

im = cv2.imread('data/images/two-women-face.jpg')  # input image = im
    
# Detect faces in the image
faceRects = faceDetector(im, 1)
print("image :", im.shape, "    {} faces detected: ".format(len(faceRects)))
```

이미지의 얼굴 좌표를 구해 해당 얼굴 부분 블러 처리하는 코드

```
# project #1 : 얼굴 부분을 블러링 처리
im_copy = im.copy()
for i in range(0, len(faceRects)):
    x1 = faceRects[i].left()
    y1 = faceRects[i].top()
    x2 = faceRects[i].right()
    y2 = faceRects[i].bottom()

    im_face = im_copy[y1:y2+1, x1:x2+1]
    im_face_blur = cv2.GaussianBlur(im_face, (0, 0), 3)
    im_copy[y1:y2+1, x1:x2+1] = im_face_blur

    plt.figure(figsize=(3,3))
    plt.imshow(im_face_blur[:,:,::-1])
    
plt.figure(figsize=(10,10))
plt.imshow(im_copy[:,:,::-1]); plt.title('face blur')
```


# 라이선스

##  프로젝트에 대한 라이선스 정보

MIT 라이선스 사용


