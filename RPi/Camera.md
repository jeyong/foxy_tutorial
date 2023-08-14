# Raspberry Pi 4 카메라 설정

- 기본 설정하는 app실행 (camera legacy interface 활성화)
```bash
sudo raspi-config 
```
   * legacy interface enable로 설정하기

- boot config 파일 확인하기
   * /boot/firmware/config.txt 파일에 아래 내용 추가되어 있는지 확인(없으면 추가하기)
```
start_x=1
gpu_mem=128
```

- 설치
```bash
sudo apt-get update
sudo apt-get install build-essential
sudo apt install cmake
```

- 빌드
```bash
mkdir ~/projects
cd ~/projects
sudo git clone https://github.com/raspberrypi/userland
cd userland
sudo ./buildme --aarch64  # --aarch64 없으면 error남!
```

- 경로설정 (~/.bashrc 파일 맨 밑에 추가하기)

```bash
export PATH=$PATH:/opt/vc/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/vc/lib
```

- 변경 적용 후 ldconfig 실행(반드시 실행해야함)

```bash
source ~/.bashrc
sudo ldconfig
```

- 리부팅 하기
- 카메라 동작 확인방법
    - Ubuntu 22.04에 설치되어 있는 Cheese 앱 실행하여 영상 들어오는지 확인