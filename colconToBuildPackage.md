# colcon 명령으로 packages 빌드하기
1. 개요
2. 실습

## 1. 개요
* 설치
```bash
sudo apt install python3-colcon-common-extensions
```

## 2. 실습
### 2-1 기초
### 2-1-1 workspace 생성
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

### 2-1-2 sources 추가하기
* 예제 코드를 src에 추가하기
```bash
cd ~/ros2_ws/src
git clone https://github.com/ros2/examples src/examples -b foxy
```

* 결과 : workspace 내부 구조
```
.
└── src
    └── examples
        ├── CONTRIBUTING.md
        ├── LICENSE
        ├── rclcpp
        ├── rclpy
        └── README.md

4 directories, 3 files
```

### 2-1-3 underlay를 source하기
```bash
source /opt/ros2/foxy/setup.bash
```
### 2-1-4 workspace 빌드하기
* 빌드하기
```bash
colcon build --symlink-install
```
* 결과
```
.
├── build
├── install
├── log
└── src

4 directories, 0 files
```

### 2-1-5 environment source 하기
* 실행
```bash
source install/setup.bash
```

### 2-1-6 빌드한 실행자 실행하기
* subscriber node 실행
```bash
ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function
```

* publisher node 실행
```bash
ros2 run examples_rclcpp_minimal_publisher publisher_member_function
```

