# jetson-yolov5_setup_for_jetpack_4.6.X
for jetson platform with jetpack, ubuntu 18.04

1. jetpack 깔기 - nvidia SDK 사용
2. ./~bashrc에  ```export OPENBLAS_CORETYPE=ARMV8 python3, export OPENBLAS_CORETYPE=ARMV8``` 추
3. opencv


# Jetson Orin 세팅

# Jetpack 설치하기

### NVIDIA SDK Manager 필요

- ubuntu가 설치된 x86기반 컴퓨터 필요 호스트 pc의 우분투 버전에 따라 설치할 수 있는 젯팩 버전이 다름

| 호스트 pc 버전 | jetpack 버전 |
| --- | --- |
| 18.04 | 4.6, 5.1 |
| 20.04 | 5.1, 6.1 |
| 22.04 | 6.1 |

### 설치 방법

- NVIDIA SDK Manager에 NVIDIA 계정 로그인 (계정 없으면 생성)
- Jepack을 설치할 Jetson 모델 선택 후 Jetpack 버젼 선택

<aside>
💡

**Jetson과 SDK 매니저 연결법**

- Jetson의 USB 포트(C 혹은 micro-5pin)와 호스트 PC를 USB로 연결
- 인식이 안될 경우 전원을 뽑은 상태서 FC REC 핀을 gnd와 쇼트
- 혹은 리커버리 진입 버튼이 있다면, 리커버리 버튼을 누른 상태로 전원 연결
</aside>

- Jetson SDK Components 항목에 체크 (안할시 CUDA 별도 설치 해야함)
- 동의에 체크 및 다운로드 → 기본 유저 이름과 비번 입력
- Jetson이 설치 중간에 부팅이 됨
- 부팅 → 로그인 → 인터넷 연결 (Host PC와 같은 공유기에 연결) → IP 주소를 Host PC에 나타난 창에 입력 → CUDA 설치
- 부팅 후 다음 명령어로 업데이트

```bash
$ sudo apt update
$ sudo apt upgrade
```

# 전원설정

- 우상단에 위치한 파워 모드를 변경해 MAXN으로 수정하기

# 파이썬 pip 패키지 설치 빌드시 오류 해결

- Jetson의 CPU 타입을 정해야함

```bash
$ gedit ~/.bashrc

# 두 줄 추가
export OPENBLAS_CORETYPE=ARMV8 python3
export OPENBLAS_CORETYPE=ARMV8
```

# 와이파이 안될 때

```bash
sudo apt install -y iwlwifi-modules
```

[J4012 Jetpack 6 No wifi](https://forum.seeedstudio.com/t/j4012-jetpack-6-no-wifi/279748/11)

# OpenCV 빌드

[Install OpenCV on Jetson Orin Nano - Q-engineering](https://qengineering.eu/install-opencv-on-orin-nano.html)

- sh 파일 일부 수정이 필요함
- **Orin Nano가 아닌, 다른 Orin 시리즈인 경우**
1. 위쪽 부분에 `if [[ $model == *"Orin"* ]]; then` 부분에서 `$model` 부분을 지우고 똑같이 `"Orin"` 으로 바꾸어서 항상 오린 설정을 적용하도록 한다.
2. 그리고 바로 안쪽의 `NO_JOB=` 뒤의 숫자을 코어 갯수+2 정도로 바꾸어 주면 더욱 빨리 빌드할 수 있다. 시간차가 많으니 꼭 하자.
3. 그냥 이걸로 하세요
    
    [OpenCV-4-10-0.sh](OpenCV-4-10-0.sh)
    

# 한글 입력 설정

[우분투 22.04 한글 입력기 설치 방법](https://staraube.tistory.com/105)

# Jtop 설치

```bash
$ sudo apt update && sudo apt upgrade
$ sudo apt install python-pip

# jetson-stats 설치
$ sudo -H pip install -U jetson-stats
$ sudo reboot

$ jtop
# jetpack 버전 확인 및 CPU, 메모리, CUDA, OpenCV 정보까지 확인 가능
```
