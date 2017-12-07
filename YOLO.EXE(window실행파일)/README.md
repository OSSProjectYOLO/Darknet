# Yolo-v2 윈도우와 리눅스 버전

[![CircleCI](https://circleci.com/gh/AlexeyAB/darknet.svg?style=svg)](https://circleci.com/gh/AlexeyAB/darknet)

1. [사용하는 방법](#how-to-use)
2. [리눅스에서 컴파일 하는 방법](#how-to-compile-on-linux)
3. [윈도우에서 컴파일 하는 방법](#how-to-compile-on-windows)
4. [훈련하는 방법 (Pascal VOC Data)](#how-to-train-pascal-voc-data)
5. [훈련하는 방법 (사용자 정의 개체를 검색하는 방법)](#how-to-train-to-detect-your-custom-objects)
6. [훈련을 중단해야 하는 때](#when-should-i-stop-training)
7. [개체 검색을 개선하는 방법](#how-to-improve-object-detection)
8. [개체의 둘러싸인 상자를 표시하고 주석 파일을 만드는 방법](#how-to-mark-bounded-boxes-of-objects-and-create-annotation-files)
9. [Yolo를 DLL로 사용하는 방법](#how-to-use-yolo-as-dll)

|  ![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png) | &nbsp; ![map_fps](https://hsto.org/files/a24/21e/068/a2421e0689fb43f08584de9d44c2215f.jpg) https://arxiv.org/abs/1612.08242 |
|---|---|

|  ![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png) | &nbsp; ![map_fps](https://hsto.org/files/3a6/fdf/b53/3a6fdfb533f34cee9b52bdd9bb0b19d9.jpg) https://arxiv.org/abs/1612.08242 |
|---|---|


# "You Only Look Once: 통합 된 실시간 객체 탐지 (version 2)"
Yolo 교차 플랫폼 Windows 및 Linux 버전 (객체 감지 용). Contributtors: https://github.com/pjreddie/darknet/graphs/contributors

이 저장소는 Linux 버전에서 포크됩니다 : https://github.com/pjreddie/darknet

더많은 세부사항 : http://pjreddie.com/darknet/yolo/

이 저장소는 다음을 지원합니다 :

* both Windows and Linux
* both OpenCV 3.x and OpenCV 2.4.13
* both cuDNN 5 and cuDNN 6
* CUDA >= 7.5
* 또한 Linux에서 SO- 라이브러리를 만들고 Windows에서 DLL 라이브러리를 만듭니다.

##### 요구사항들:
* **Linux GCC>=4.9 or Windows MS Visual Studio 2015 (v140)**: https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409  (or offline [ISO image](https://go.microsoft.com/fwlink/?LinkId=615448&clcid=0x409))
* **CUDA 8.0**: https://developer.nvidia.com/cuda-downloads
* **OpenCV 3.x**: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.2.0/opencv-3.2.0-vc14.exe/download
* **or OpenCV 2.4.13**: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/2.4.13/opencv-2.4.13.2-vc14.exe/download
  - OpenCV allows to show image or video detection in the window and store result to file that specified in command line `-out_filename res.avi`
* **GPU with CC >= 2.0** if you use CUDA, or **GPU CC >= 3.0** if you use cuDNN + CUDA: https://en.wikipedia.org/wiki/CUDA#GPUs_supported

##### 다양한 cfg 파일에 대한 사전 학습 된 모델을 다운로드 할 수 있습니다 (더 작은 용량 -> 더 빠르고 낮은 품질):
* `yolo.cfg` (194 MB COCO-model) - require 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo.weights
* `yolo-voc.cfg` (194 MB VOC-model) - require 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo-voc.weights
* `tiny-yolo.cfg` (60 MB COCO-model) - require 1 GB GPU-RAM: http://pjreddie.com/media/files/tiny-yolo.weights
* `tiny-yolo-voc.cfg` (60 MB VOC-model) - require 1 GB GPU-RAM: http://pjreddie.com/media/files/tiny-yolo-voc.weights
* `yolo9000.cfg` (186 MB Yolo9000-model) - require 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo9000.weights

컴파일 된 것을 darknet.exe 근처에 놓으십시오.

경로별로 cfg 파일을 얻을 수 있습니다  : `darknet/cfg/`

##### 결과의 예 :

[![Everything Is AWESOME](http://img.youtube.com/vi/VOC3huqHrss/0.jpg)](https://www.youtube.com/watch?v=VOC3huqHrss "Everything Is AWESOME")

기타 : https://www.youtube.com/channel/UC7ev3hNVkx4DzZ3LO19oebg

### 사용하는 방법 :

##### Example of usage in cmd-files from `build\darknet\x64\`:

* `darknet_voc.cmd` - 194MB VOC 모델 yolo-voc.weights 및 yolo-voc.cfg로 초기화하고 이미지 파일의 이름을 입력하기를 기다리는 중.
* `darknet_demo_voc.cmd` - 194MB VOC 모델 yolo-voc.weights 및 yolo-voc.cfg로 초기화하고 이름을 바꾸어야하는 비디오 파일을 재생. test.mp4
* `darknet_demo_store.cmd` - 194MB VOC 모델 yolo-voc.weights 및 yolo-voc.cfg로 초기화하고 이름을 바꾸어야하는 비디오 파일을 재생 : test.mp4, 결과 저장 : res.avi
* `darknet_net_cam_voc.cmd` - 194MB VOC 모델로 초기화, 네트워크 비디오 카메라 mjpeg-stream (또한 휴대 전화로)에서 비디오 재생.
* `darknet_web_cam_voc.cmd` - 194MB VOC 모델로 초기화, 웹 카메라 번호 # 0에서 비디오 재생.
* `darknet_coco_9000.cmd` - 186 MB Yolo9000 COCO 모델로 초기화하고 이미지에 탐지를 표시. dog.jpg
* `darknet_coco_9000_demo.cmd` - 186 MB Yolo9000 COCO 모델로 초기화하고 비디오 (존재하는 경우) : street4k.mp4에 대한 감지를 표시하고 결과를 res.avi에 저장.

##### cmd-files에서의 사용 예 :

Linux 사용시 `./darknet` 대신 `darknet.exe`, 이렇게 : `./darknet detector test ./cfg/coco.data ./cfg/yolo.cfg ./yolo.weights`

* 194 MB COCO-model - image: `darknet.exe detector test data/coco.data yolo.cfg yolo.weights -i 0 -thresh 0.2`
* Alternative method 194 MB COCO-model - image: `darknet.exe detect yolo.cfg yolo.weights -i 0 -thresh 0.2`
* 194 MB VOC-model - image: `darknet.exe detector test data/voc.data yolo-voc.cfg yolo-voc.weights -i 0`
* 194 MB COCO-model - video: `darknet.exe detector demo data/coco.data yolo.cfg yolo.weights test.mp4 -i 0`
* 194 MB VOC-model - video: `darknet.exe detector demo data/voc.data yolo-voc.cfg yolo-voc.weights test.mp4 -i 0`
* 194 MB COCO-model - **save result to the file res.avi**: `darknet.exe detector demo data/coco.data yolo.cfg yolo.weights test.mp4 -i 0 -out_filename res.avi`
* 194 MB VOC-model - **save result to the file res.avi**: `darknet.exe detector demo data/voc.data yolo-voc.cfg yolo-voc.weights test.mp4 -i 0 -out_filename res.avi`
* Alternative method 194 MB VOC-model - video: `darknet.exe yolo demo yolo-voc.cfg yolo-voc.weights test.mp4 -i 0`
* 60 MB VOC-model for video: `darknet.exe detector demo data/voc.data tiny-yolo-voc.cfg tiny-yolo-voc.weights test.mp4 -i 0`
* 194 MB COCO-model for net-videocam - Smart WebCam: `darknet.exe detector demo data/coco.data yolo.cfg yolo.weights http://192.168.0.80:8080/video?dummy=param.mjpg -i 0`
* 194 MB VOC-model for net-videocam - Smart WebCam: `darknet.exe detector demo data/voc.data yolo-voc.cfg yolo-voc.weights http://192.168.0.80:8080/video?dummy=param.mjpg -i 0`
* 194 MB VOC-model - WebCamera #0: `darknet.exe detector demo data/voc.data yolo-voc.cfg yolo-voc.weights -c 0`
* 186 MB Yolo9000 - image: `darknet.exe detector test cfg/combine9k.data yolo9000.cfg yolo9000.weights`
* 186 MB Yolo9000 - video: `darknet.exe detector demo cfg/combine9k.data yolo9000.cfg yolo9000.weights test.mp4`
* 이미지 목록을 처리하려면 `image_list.txt` 탐지의 결과  `result.txt` 사용:
    `darknet.exe detector test data/voc.data yolo-voc.cfg yolo-voc.weights < image_list.txt > result.txt`
    이 선을 주석 처리하여 각 이미지에 ESC 버튼을 누르지 않아도됩니다 : https://github.com/AlexeyAB/darknet/blob/6ccb41808caf753feea58ca9df79d6367dedc434/src/detector.c#L509

##### 모든 Android 스마트 폰에서 네트워크 비디오 카메라 mjpeg-stream을 사용하는 경우 :

1. Android phone mjpeg-stream soft 용 다운로드 : IP Webcam / Smart WebCam


    * Smart WebCam - preferably: https://play.google.com/store/apps/details?id=com.acontech.android.SmartWebCam2
    * IP Webcam: https://play.google.com/store/apps/details?id=com.pas.webcam

2. Android 폰을 Wi-Fi (WiFi-router를 통해) 또는 USB를 통해 컴퓨터에 연결하십시오.
3. 스마트 웹캠을 휴대 전화에서 시작하십시오.
4. 전화 응용 프로그램 (Smart WebCam)에 표시된 주소를 아래에서 바꾸고 실행하십시오.


* 194 MB COCO-model: `darknet.exe detector demo data/coco.data yolo.cfg yolo.weights http://192.168.0.80:8080/video?dummy=param.mjpg -i 0`
* 194 MB VOC-model: `darknet.exe detector demo data/voc.data yolo-voc.cfg yolo-voc.weights http://192.168.0.80:8080/video?dummy=param.mjpg -i 0`

### 리눅스에서 컴파일하는 방법 :

darknet에서  `make` 실행
make를하기 전에, `Makefile`: [link](https://github.com/AlexeyAB/darknet/blob/9c1b9a2cf6363546c152251be578a21f3c3caec6/Makefile#L1)
* `GPU=1` GPU를 사용하여 CUDA로 가속화 (CUDA가 있어야합니다.  `/usr/local/cuda`)
* `CUDNN=1` cuDNN v5 / v6으로 구축하여 GPU를 사용하여 교육 시간 단축 (cuDNN이 있어야합니다.  `/usr/local/cudnn`)
* `OPENCV=1` OpenCV 3.x / 2.4.x로 구축 - 네트워크 카메라 또는 웹캠에서 비디오 파일과 비디오 스트림을 감지 할 수 있습니다.
* `DEBUG=1` Yolo의 디버그 버전을 빌드하는 방법
* `OPENMP=1` 멀티 코어 CPU를 사용하여 Yolo 가속화를위한 OpenMP 지원 구축
* `LIBSO=1` to build a library `darknet.so` and binary runable file `uselib` that uses this library. 또는 그렇게 실행하려고 할 수 있습니다. `LD_LIBRARY_PATH=./:$LD_LIBRARY_PATH ./uselib test.mp4`  코드에서 이 SO 라이브러리를 사용하는 법 -  C ++ 예제를 볼 수 있습니다 : https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp


### Windows에서 컴파일하는 방법 :

1. ** MSVS 2015, CUDA 8.0 및 OpenCV 3.0을 보유한 경우 **  (with paths: `C:\opencv_3.0\opencv\build\include` & `C:\opencv_3.0\opencv\build\x64\vc14\lib`), MSVS를 시작하고 open
`build\darknet\darknet.sln`, set **x64** 그리고 **Release**, 다음을 진행 : Build -> Build darknet

1.1. 파일들을 찾는다 `opencv_world320.dll` 와  `opencv_ffmpeg320_64.dll` 에서 `C:\opencv_3.0\opencv\build\x64\vc14\bin` 그리고  `darknet.exe` 가까이 둔다.

2. 다른 버전이 있다면  **CUDA (not 8.0)** 그때 다음을 연다.  `build\darknet\darknet.vcxproj` 메모장을 사용하여 "CUDA 8.0"으로 2 개 장소를 찾고 CUDA 버전으로 변경 한 다음 1 단계 수행

3. **GPU**가 없지만 **MSVS 2015 및 OpenCV 3.0이있는 경우** (with paths: `C:\opencv_3.0\opencv\build\include` & `C:\opencv_3.0\opencv\build\x64\vc14\lib`), MSVS를 시작하고 open
`build\darknet\darknet_no_gpu.sln`, set **x64** 그리고 **Release**, 다음을 실행 : Build -> Build darknet


4. 3.0 대신에 **OpenCV 2.4.13**을 가지고 있다면, 이후에 pathes를 변경. 변경 후 `\darknet.sln` 이 열림.

    4.1 (프로젝트에서 오른쪽 클릭) -> 속성 -> C / C ++ -> 일반 -> 추가 포함 디렉토리 :  `C:\opencv_2.4.13\opencv\build\include`
  
    4.2 (프로젝트에서 마우스 오른쪽 버튼 클릭) -> 속성 -> 링커 -> 일반 -> 추가 라이브러리 디렉토리 : `C:\opencv_2.4.13\opencv\build\x64\vc14\lib`
  
5. 속도 향상을 위해 CUDNN으로 빌드하려면 다음을 수행.
      
    * 다운로드 및 설치  **cuDNN 6.0 for CUDA 8.0** : https://developer.nvidia.com/cudnn
      
      * Windows 시스템 변수`cudnn`에 CUDNN의 경로를 추가 : https://hsto.org/files/a49/3dc/fc4/a493dcfc4bd34a1295fd15e0e2e01f26.jpg
      
      *  `\darknet.sln` 실행 -> (프로젝트를 마우스 오른쪽 버튼으로 클릭)-> properties  -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add at the beginning of line: `CUDNN;`

### 컴파일하는 법 (custom) :

또한 자신 만의`darknet.sln`과`darknet.vcxproj`를 만들 수 있습니다. 이 예제는 CUDA 8.0과 OpenCV 3.0입니다.

그런 다음 생성 된 프로젝트에 추가.
- (프로젝트를 마우스 오른쪽 단추로 클릭) -> properties  -> C/C++ -> General -> Additional Include Directories, put here:

`C:\opencv_3.0\opencv\build\include;..\..\3rdparty\include;%(AdditionalIncludeDirectories);$(CudaToolkitIncludeDir);$(cudnn)\include`
- (프로젝트를 마우스 오른쪽 단추로 클릭) -> Build dependecies -> Build Customizations -> set check on CUDA 8.0 or what version you have - for example as here: http://devblogs.nvidia.com/parallelforall/wp-content/uploads/2015/01/VS2013-R-5.jpg
- `\ src`에서 모든 .c & .cu 파일을 프로젝트에 추가.
- (프로젝트를 마우스 오른쪽 단추로 클릭)  -> properties  -> Linker -> General -> Additional Library Directories, put here:

`C:\opencv_3.0\opencv\build\x64\vc14\lib;$(CUDA_PATH)lib\$(PlatformName);$(cudnn)\lib\x64;%(AdditionalLibraryDirectories)`
-  (프로젝트를 마우스 오른쪽 단추로 클릭)  -> properties  -> Linker -> Input -> Additional dependecies, put here:

`..\..\3rdparty\lib\x64\pthreadVC2.lib;cublas.lib;curand.lib;cudart.lib;cudnn.lib;%(AdditionalDependencies)`
- (프로젝트를 마우스 오른쪽 단추로 클릭) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions

`OPENCV;_TIMESPEC_DEFINED;_CRT_SECURE_NO_WARNINGS;_CRT_RAND_S;WIN32;NDEBUG;_CONSOLE;_LIB;%(PreprocessorDefinitions)`

- `\ src \ detector.c` 파일을 열고`#pragma`와`# inclue`를 OpenCV로 검사.

- .exe (X64 및 Release)로 컴파일하고 .dll-s를 .exe와 가까이 위치.

    * `pthreadVC2.dll, pthreadGC2.dll` from \3rdparty\dll\x64

* `cusolver64_80.dll, curand64_80.dll, cudart64_80.dll, cublas64_80.dll` - CUDA 8.0 또는 사용자 버전의 경우 : 80, 다음 경로 확인 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin

    * For OpenCV 3.X: `opencv_world320.dll` and `opencv_ffmpeg320_64.dll` from `C:\opencv_3.0\opencv\build\x64\vc14\bin` 
    * For OpenCV 2.4.13: `opencv_core2413.dll`, `opencv_highgui2413.dll` and `opencv_ffmpeg2413_64.dll` from  `C:\opencv_2.4.13\opencv\build\x64\vc14\bin`

## Pascal VOC Data를 이용한 방법 :

1. 콘볼루션 계층의 미리 정해놓은 가중치 다운 (76 MB): http://pjreddie.com/media/files/darknet19_448.conv.23 and put to the directory `build\darknet\x64`

2.Pascal VOC Data를 다운로드하고 `build\darknet\x64\data\voc` 생성된 디렉토리 확인  `build\darknet\x64\data\voc\VOCdevkit\`:
    * http://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
    * http://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
    * http://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
    
    2.1 Download file `voc_label.py` to dir `build\darknet\x64\data\voc`: http://pjreddie.com/media/files/voc_label.py

3. Windows 용 Python 다운로드 및 설치 : https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe

4. 실행 명령어 : `python build\darknet\x64\data\voc\voc_label.py` (to generate files: 2007_test.txt, 2007_train.txt, 2007_val.txt, 2012_train.txt, 2012_val.txt)

5. 실행 명령어 : `type 2007_train.txt 2007_val.txt 2012_*.txt > train.txt`

6. Set `batch=64` and `subdivisions=8` in the file `yolo-voc.2.0.cfg`: [link](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/yolo-voc.2.0.cfg#L2)

7. 다음 명령어를 입력하여 훈련을 시작하거나  `train_voc.cmd` 커멘드 라인에 다음을 입력하여 시작한다 : `darknet.exe detector train data/voc.data yolo-voc.2.0.cfg darknet19_448.conv.23`

필요한 경우 파일에서 경로 변경 `build\darknet\x64\data\voc.data`

추가정보를 얻고 싶으시면 다음 링크를 참고 : http://pjreddie.com/darknet/yolo/#train-voc

## 멀티 GPU로 훈련하는 방법 :

1. 한개의 GPU에서 우선적으로 훈련 : `darknet.exe detector train data/voc.data yolo-voc.2.0.cfg darknet19_448.conv.23`

2. 그런 다음 부분적으로 훈련 된 모델을 사용하여 중지하고 `/backup/yolo-voc_1000.weights`  멀티GPU를  (최대 4 GPU)로 교육을 실행  `darknet.exe detector train data/voc.data yolo-voc.2.0.cfg /backup/yolo-voc_1000.weights -gpus 0,1,2,3`

더 자세한 정보는 다음 사이트에서 참고 : https://groups.google.com/d/msg/darknet/NbJqonJBTSY/Te5PfIpuCAAJ

## 사용자 지정 개체를 탐지하기 위한 훈련 방법

1.  `yolo-voc.2.0.cfg`와 동일한 내용으로 `yolo-obj.cfg` 파일을 만들거나  `yolo-obj.cfg`에   `yolo-voc.2.0.cfg`를 복사하고 다음을 수행.

  * batch의 내용을 변경  [`batch=64`](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/yolo-voc.2.0.cfg#L2)
  * subdivisions의 내용을 변경  [`subdivisions=8`](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/yolo-voc.2.0.cfg#L3)
  * `class = 20` 줄은 사용자의 객체 수로 변경
  * change line #237 from [`filters=125`](https://github.com/AlexeyAB/darknet/blob/master/cfg/yolo-voc.2.0.cfg#L224) to: filters=(classes + 5)*5, so if `classes=2` then should be `filter=35`
  
  (일반적으로`filters '는`classes`,`num` 및`coords`에 의존합니다. 즉`(classes + coords + 1) * num`과 같습니다.

  예를 들어, 2 개의 객체의 경우,`yolo-obj.cfg` 파일은`yolo-voc.2.0.cfg`와 다를 수 있음 :

  ```
  [convolutional]
  filters=35

  [region]
  classes=2
  ```

2. `build \ darknet \ x64 \ data \`디렉토리에`obj.names` 파일을 만듭니다.
    객체 이름은 - 각각 새로운 행에 있음.


3. ** classes \ object의 수 **를 포함하는`build \ darknet \ x64 \ data \`디렉토리에`obj.data` 파일을 생성 :


  ```
  classes= 2
  train  = data/train.txt
  valid  = data/test.txt
  names = data/obj.names
  backup = backup/
  ```

4. `build \ darknet \ x64 \ data \ obj \`디렉토리에 오브젝트의 이미지 파일 (.jpg)을 삽입.


5. `.jpg`-image-file에 대해서`.txt` 파일을 만든다 - 같은 디렉토리에 있고 같은 이름이지만 확장자는`.txt`이며, 파일에 넣으십시오 :이 이미지의 객체 번호와 객체 좌표 새로운 줄에있는 각 객체에 대해 : <object-class> <x> <y> <width> <height>`


  Where: 
  *`<object-class>`- '0'에서`(classes-1)`까지의 객체 정수
  *`<x> <y> <width> <height>`- 이미지의 폭과 높이를 기준으로 한 부동 소수점 값으로, 0.0에서 1.0까지 동일 할 수 있습니다.
  * 예 :`<x> = <absolute_x> / <image_width>`또는`<height> = <absolute_height> / <image_height>`
  * atention :`<x> <y>`- 사각형의 중심 (왼쪽 위 모서리가 아님)

예를 들어`img1.jpg '의 경우 다음을 포함하는`img1.txt`를 생성 :


  ```
  1 0.716797 0.395833 0.216406 0.147222
  0 0.687109 0.379167 0.255469 0.158333
  1 0.420312 0.395833 0.140625 0.166667
  ```

6. `build \ darknet \ x64 \ data \`디렉토리에`train.txt` 파일을 만든다. 이미지의 파일명, 각 파일명은`darknet.exe '에 상대적인 새로운 줄의 경로로 만들며  예를 들면 다음과 같다  :


  ```
  data/obj/img1.jpg
  data/obj/img2.jpg
  data/obj/img3.jpg
  ```

7. 콘볼루션 계층의 미리 정해놓은 가중치 다운 (76 MB): http://pjreddie.com/media/files/darknet19_448.conv.23 and put to the directory `build\darknet\x64`

8. 명령어 라인을 사용하여 훈련을 시작 : `darknet.exe detector train data/obj.data yolo-obj.cfg darknet19_448.conv.23`

    (파일`yolo-obj_xxx.weights`는 1000 반복이 도달 할 때까지 그리고 각 1000 반복 후에 100 반복마다`build \ darknet \ x64 \ backup \에 저장 될 것입니다)

9. 훈련이 끝나면`build \ darknet \ x64 \ backup \`경로에서`yolo-obj_final.weights` 결과를 얻습니다.


* 1000 번 반복 한 후에는이 시점부터 시작하여 나중에 시작할 수 있습니다. 예를 들어 2000 회 반복 한 후에는 교육을 중지하고 나중에 build \ darknet \ x64 \ backup \에서`yolo-obj_2000.weights`를`build \ darknet \ x64 \ '로 복사하고`darknet'을 사용하여 교육을 시작할 수 있습니다. exe 검출기 기차 데이터 / obj.data yolo-obj.cfg yolo-obj_2000.weights`

* 또한 모든 45000회의 반복보다 빠른 결과를 얻을 수 있습니다.

 
 ## 훈련을 중지해야 하는 시기:

일반적으로 각 클래스(객체)에 대해 2000회 반복적으로 반복됩니다. 그러나 교육을 중단해야 할 때 보다 정확한 정의를 위해 다음 매뉴얼을 사용하십시오.

1. 교육 과정에서 다양한 오류 표시등이 나타날 것이며**0.060730 avg**를 더 이상 줄이지 않을 때는 중지해야 합니다

  > Region Avg IOU: 0.798363, Class: 0.893232, Obj: 0.700808, No Obj: 0.004567, Avg Recall: 1.000000,  count: 8
  > Region Avg IOU: 0.800677, Class: 0.892181, Obj: 0.701590, No Obj: 0.004574, Avg Recall: 1.000000,  count: 8
  >
  > **9002**: 0.211667, **0.060730 avg**, 0.001000 rate, 3.868000 seconds, 576128 images
  > Loaded: 0.000000 seconds

  * **9002** - iteration number (number of batch)
  * **0.060730 avg** - average loss (error) - **the lower, the better**

평균 손실**0.274 xxxavg**가 더 이상 반복적으로 감소하지 않는 경우에는 교육을 중단해야 합니다.

2. 일단 훈련이 중단되면, 당신은 다음과 같은 것들 중에서 마지막으로 `werket\build\x6\\\ba\backup` 을 선택하그 중에서 가장 좋은 것을 선택해야 한다.


예를 들어, 9000회 반복 작업을 중지한 후에는 최상의 결과를 얻을 수 있습니다. 최상의 결과는 이전의 가중치(7000, 8,000, 9000)입니다. 그것은 지나치게 과한 것으로 인해 발생할 수 있다. **overfitting**-trainingdata에서 물체의 이미지를 감지할 수 있지만 다른 영상에서는 물체를 감지할 수 없습니다. **StopPoint****에서 가중치를 얻어야 합니다.

![Overfitting](https://hsto.org/files/5dc/7ae/7fa/5dc7ae7fad9d4e3eb3a484c58bfc1ff5.png) 

초기 정지 지점에서 가중치을 구하려면:

2.1. 처음에는 파일`obj.data`에서 유효성 검사 데이터 셋`valid = valid.txt` (`train.txt`에서와 같이`valid.txt` 형식)을 지정해야합니다. valid image,`data\train.txt`를 `data\valid.txt`에 복사하십시오.

2. 29000회 반복 후에 훈련이 중단된 경우, 이전의 가중치를 확인하기 위해 다음과 같은 명령을 사용한다.


* `darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_7000.weights`
* `darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_8000.weights`
* `darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_9000.weights`

각 가중치에 대한 최종 출력 라인(7000, 8,000, 9000):

> 7586 7612 7689 RPs/Img: 68.23 **IOU: 77.86%** Recall:99.00%

* **IOU** - 크기가 클수록 정확도가 높음 - **사용하기가 더 편리함**
* **RECALL** - 크면 클수록, 더 좋습니다 (정확도에 대해 말합니다). 실제로 Yolo는 긍정적으로 계산하므로 사용되어서는 안됩니다.


예를 들어, **더 큰 IOU**는 `yolo-obj_8000.weights`에 가중치를 부여한 다음 **가중치를 사용하여 탐지합니다**.


![precision_recall_iou](https://hsto.org/files/ca8/866/d76/ca8866d76fb840228940dbf442a7f06a.jpg)

**mAP**계산하는 방법 [voc_eval.py](https://github.com/AlexeyAB/darknet/blob/master/scripts/voc_eval.py) or [datascience.stackexchange link](https://datascience.stackexchange.com/questions/16797/what-does-the-notation-map-5-95-mean)

###사용자 정의 객체 탐지:

사용자 정의 객체 탐지의 예 : `darknet.exe detector test data / obj.data yolo-obj.cfg yolo-obj_8000.weights`


| ![Yolo_v2_training](https://hsto.org/files/d12/1e7/515/d121e7515f6a4eb694913f10de5f2b61.jpg) | ![Yolo_v2_training](https://hsto.org/files/727/c7e/5e9/727c7e5e99bf4d4aa34027bb6a5e4bab.jpg) |
|---|---|

## How to improve object detection:

1. Before training:
  * set flag `random=1` in your `.cfg`-file - it will increase precision by training Yolo for different resolutions: [link]https://github.com/AlexeyAB/darknet/blob/master/cfg/yolo-voc.2.0.cfg#L244)
  
  * desirable that your training dataset include images with objects at diffrent: scales, rotations, lightings, from different sides

2. After training - for detection:

  * Increase network-resolution by set in your `.cfg`-file (`height=608` and `width=608`) or (`height=832` and `width=832`) or (any value multiple of 32) - this increases the precision and makes it possible to detect small objects: [link](https://github.com/AlexeyAB/darknet/blob/master/cfg/yolo-voc.2.0.cfg#L4)
  
    * you do not need to train the network again, just use `.weights`-file already trained for 416x416 resolution
    * if error `Out of memory` occurs then in `.cfg`-file you should increase `subdivisions=16`, 32 or 64: [link](https://github.com/AlexeyAB/darknet/blob/master/cfg/yolo-voc.2.0.cfg#L3)

## How to mark bounded boxes of objects and create annotation files:

Here you can find repository with GUI-software for marking bounded boxes of objects and generating annotation files for Yolo v2: https://github.com/AlexeyAB/Yolo_mark

With example of: `train.txt`, `obj.names`, `obj.data`, `yolo-obj.cfg`, `air`1-6`.txt`, `bird`1-4`.txt` for 2 classes of objects (air, bird) and `train_obj.cmd` with example how to train this image-set with Yolo v2

## How to use Yolo as DLL

1. To compile Yolo as C++ DLL-file `yolo_cpp_dll.dll` - open in MSVS2015 file `build\darknet\yolo_cpp_dll.sln`, set **x64** and **Release**, and do the: Build -> Build yolo_cpp_dll
    * You should have installed **CUDA 8.0**
    * To use cuDNN do: (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add at the beginning of line: `CUDNN;`

2. To use Yolo as DLL-file in your C++ console application - open in MSVS2015 file `build\darknet\yolo_console_dll.sln`, set **x64** and **Release**, and do the: Build -> Build yolo_console_dll

    * you can run your console application from Windows Explorer `build\darknet\x64\yolo_console_dll.exe`
    * or you can run from MSVS2015 (before this - you should copy 2 files `yolo-voc.cfg` and `yolo-voc.weights` to the directory `build\darknet\` )
    * after launching your console application and entering the image file name - you will see info for each object: 
    `<obj_id> <left_x> <top_y> <width> <height> <probability>`
    * to use simple OpenCV-GUI you should uncomment line `//#define OPENCV` in `yolo_console_dll.cpp`-file: [link](https://github.com/AlexeyAB/darknet/blob/a6cbaeecde40f91ddc3ea09aa26a03ab5bbf8ba8/src/yolo_console_dll.cpp#L5)
    * you can see source code of simple example for detection on the video file: [link](https://github.com/AlexeyAB/darknet/blob/ab1c5f9e57b4175f29a6ef39e7e68987d3e98704/src/yolo_console_dll.cpp#L75)
   
`yolo_cpp_dll.dll`-API: [link](https://github.com/AlexeyAB/darknet/blob/master/src/yolo_v2_class.hpp#L42)
```
class Detector {
public:
	Detector(std::string cfg_filename, std::string weight_filename, int gpu_id = 0);
	~Detector();

	std::vector<bbox_t> detect(std::string image_filename, float thresh = 0.2, bool use_mean = false);
	std::vector<bbox_t> detect(image_t img, float thresh = 0.2, bool use_mean = false);
	static image_t load_image(std::string image_filename);
	static void free_image(image_t m);

#ifdef OPENCV
	std::vector<bbox_t> detect(cv::Mat mat, float thresh = 0.2, bool use_mean = false);
#endif
};
```
