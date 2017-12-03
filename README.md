# Darknet YOLO API Instruction
Open Source SW 02 Class Team Project

## 1. YOLO API란?
객체 탐지 기법에 있어서 새로운 접근법인 YOLO를 소개합니다. 

기존 객체 탐지 기법은 사전 작업으로 탐지를 먼저 수행합니다. 
여기서 YOLO API 시스템은 객체 탐지를 공간적으로 분리된 경계공간들과 class(분류할 object 종류들)에 대한 확률과 연관된 회귀문제로 재정의하였습니다. 
단일 신경망 네트워크는 전체 이미지에서 한번의 평가를 통해서 직접적으로 경계공간들을 예측하고 class의 확률을 계산합니다. 
전체 탐지 파이프라인이 단일 네트워크이기 때문에, 탐지 성능이 최적화됩니다. 

YOLO API의 통합된 아키텍쳐는 매우 빠르게 수행이 됩니다. YOLO model은 45 FPS로 실시간 이미지 연산이 가능합니다. 
또한 더 작은 버젼의 네트워크인 Fast YOLO는 매우 놀랍게도 다른 실시간 탐지모델보다 2배의 mAP(Mean Accuracy Precision:: 평균 정확도)를 가지면서 155 FPS의 성능을 보여줍니다.
최신의 탐지 시스템들과 비교했을 때, YOLO는 localization error가 조금 더 높지만, 배경으로 인한 예측 실패율은 더 낮습니다. 
마지막으로 YOLO API는 탐지의 아주 일반적인 표현들을 학습합니다. 이 말은 DPM이나 R-CNN같은 다른 탐지 대비 artwork같은 다른 영역에서의 자연스러운 이미지로부터 일반적인 표현을 학습하는데 있어서 결과가 더 좋다는 것을 의미합니다.

## 2. 구성
* 웹사이트 제작 : http://khseob0715.dothome.co.kr/YOLO/
* Latex 매뉴얼 작성 - YOLO API Web Instruction/darknet_YOLO 폴더 
                     https://github.com/OSSProjectYOLO/Darknet/tree/master/YOLO%20API%20Web%20Instruction/darknet_YOLO
* 해당 README.md는 Markdown으로 작성하였습니다.

## 3. 참고문헌
* Ali Farhadi Joseph Redmon.YOLO9000: Better, Faster, Stronger.  San Val, 2016 : https://arxiv.org/abs/1612.08242

| 팀원        | 학번      | GitHub아이디  |
| :----      | :----     | :----         | 
| 이대경(팀장)| Data      | cocobino      |
| 김한섭      | 20134822  | khseob0715(master 계정)  |
| 강일송      | 20134845  | Borngroundg  |
