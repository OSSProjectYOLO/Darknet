# Darknet YOLO API Instruction
Open Source SW 02 Class Team Project

## 1. YOLO API란?
객체 탐지 기법에 있어서 새로운 접근법인 YOLO를 소개합니다.

기존 객체 탐지 기법은 사전 작업으로 탐지를 먼저 수행합니다.<br>
하지만 YOLO API 시스템은 객체 탐지를 공간적으로 분리된 경계공간들과 class(분류할 object 종류들)에 대한 확률과 연관된 회귀문제로 재정의하였습니다.
API의 단일 신경망 네트워크는 전체 이미지에서 한번의 평가를 통해서 직접적으로 경계공간들을 예측하고 class의 확률을 계산합니다.
또한 전체 탐지 파이프라인이 단일 네트워크이기 때문에, 탐지 성능이 최적화됩니다. <br>

YOLO API의 통합된 아키텍쳐는 매우 빠르게 수행이 되는데 45 FPS로 실시간 이미지 연산이 가능합니다.
또한 다른 버전인 Fast YOLO는 놀랍게도 다른 실시간 탐지모델보다 2배의 mAP(평균 정확도)를 가지면서 155 FPS의 성능을 보여줍니다. <br>
최신 탐지시스템과 비교했을 때, YOLO는 localization error가 조금 더 높지만, 배경으로 인한 예측 실패율은 더 낮습니다. <br>

마지막으로 YOLO API의 장점은 탐지의 아주 일반적인 표현들을 학습합니다.
이 말은 DPM이나 R-CNN같은 다른 탐지 대비 다른 영역에서의 자연스러운 이미지로부터 일반적인 표현을 학습하는데 있어서 결과가 더 좋다는 것을 의미합니다.

## 2. YOLO API를 선택한 이유
팀원 중 한명이 Computer vision 분야에 대한 관심이 많아 예전부터 알고 있던 API였습니다. <br>
하지만 당시 해당 팀원은 Python으로 구현된 프로그램과 수업 이전 Github 사용법을 몰랐기 때문에 <br>
YOLO API가 어렵게만 느껴져 해당 API를 전혀 활용해보지 못했다는 이야기를 들었습니다. <br>
그렇기에 아쉬움이 남는다고 하여 저희 팀은 이 YOLO API를 선택하게 되었고 <br>
Python 프로그래밍과 OpenCV, Computer Vision 분야에 대해서 함께 Study를 하기로 하였습니다. <br>

그렇지만 무엇보다도 API의 이름이 너무 마음에 들었습니다.  <br>
요즘 라이프스타일 트렌드인 YOLO(You Only Live One)와 이름이 비슷한 **You Only Look Once인 YOLO API!**<br>

팀 프로젝트를 팀원들 모두 **재미있게 즐기면서 하자**는 의미에서 선택을 하였습니다.

## 3.YOLO Window 실행 환경 사용법
- **MSVS 2015, CUDA 8.0, OPENCV 3.0** 을 사용 중이라면 Path 설정을 다음과 같이 해줍니다.
**(C:\opencv_3.0\opencv\build\include
  & C:\opencv_3.0\opencv\build\x64\vc14\lib)**

- **opencv_world320.dll , opencv_ffmpeg320_64.dll** 파일을 **C:\opencv_3.0\opencv\build\x64\vc14\bin** 에 있는 실행파일에 옮겨줍니다.

- 만약에 다른 **CUDA (not 8.0)** 버전이라면 **build\darknet\darknet.vcxproj** 파일을 노트패드로 열어서 CUDA 8.0 에 Ver.2 로 되있는 값을 Ver.1 로 바꿔줍니다.

- 만약에 **GPU(그래픽카드)** 가 없는경우에는 **MSVS 2015, OpenCV 3.0** 의 Path 설정을 **C:\opencv_3.0\opencv\build\include & C:\opencv_3.0\opencv\build\x64\vc14\lib** 으로 해주고 MSVS를 실행해줍니다.
그리고 **build\darknet\darknet_no_gpu.sln** 의 **x64** 와 **Release** 설정을 : Build -> Build darknet 으로 수정합니다.

- 만약 **OpenCV 2.1.13** 을 사용한다면 (3.0이외 버전 포함) **\darknet.sln** 파일을 열어 Path 설정을 다음과 같이 해줍니다
  -  (right click on project) -> properties -> C/C++ -> General -> Additional Include Directories: C:\opencv_2.4.13\opencv\build\include
  - (right click on project) -> properties -> Linker -> General -> Additional Library Directories: C:\opencv_2.4.13\opencv\build\x64\vc14\lib

- CUDNN 의 속도를 향상 시키고 싶으시다면 다음과 절차를 따르시면 됩니다.
  - **cuDNN 6.0 for CUDA 8.0** 설치하면 됩니다 : https://developer.nvidia.com/cudnn
  - https://hsto.org/files/a49/3dc/fc4/a493dcfc4bd34a1295fd15e0e2e01f26.jpg
  -  \darknet.sln 파일을 연 후 -> (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions을 열어서 다음내용을 추가해줍니다.



## 4. 구성
* Latex 매뉴얼 작성 : https://github.com/OSSProjectYOLO/Darknet/tree/master/darknet_YOLO
* 웹사이트 제작 : http://khseob0715.dothome.co.kr/YOLO/
* 해당 README.md는 Markdown으로 작성하였습니다.
* 실행파일 YOLO.EXE(window실행파일) 은 윈도우 환경에서 YOLO 프로그램 실행을 지원합니다.



## 5. 참고문헌
* Ali Farhadi Joseph Redmon.YOLO9000: Better, Faster, Stronger.  San Val, 2016 : https://arxiv.org/abs/1612.08242
<br>
<br>

| 팀원        | 학번      | GitHub아이디  |
| :----      | :----     | :----         |
| 이대경(팀장)| 20124956  | cocobino      |
| 강일송      | 20134845  | Borngroundg  |
| 김한섭      | 20134822  | khseob0715(master 계정)  |

## 6. 협업 증빙
![](http://imageshack.com/a/img923/6836/XNOwtM.jpg)
