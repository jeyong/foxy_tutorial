# workspace 생성하기
1. 개요
2. 실습


## 1. 개요
* 

## 2. 실습
### 2-1 ROS2 환경 source 하기

```bash
source /opt/ros/foxy/setup.bash
```
### 2-2 새 directory 생성하기
* ros2_ws
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```
  * 새로운 workspace를 위해서 새로운 directory 생성
  * workspace 이름 생성 : 목적에 맞게 이름 정하기

### 2-3 샘플 repo clone하기
* ros2_ws/src 디렉토리 내부에 소스 받아오기
```bash
cd ~/ros2_ws/src
git clone https://github.com/ros/ros_tutorials.git -b foxy-devel
```

### 2-4 의존성 해결
* workspace 빌드하기 전에 package 의존성 확인 작업이 필요
* 의존성에 문제가 있는 경우
  * ROS 2의 경우 package에 따라서 빌드 시간이 올래 걸릴 수 있음. 실컷 10분 빌드하고 나서 의존성에 문제가 있다는 것을 알게 되면 수정 후 다시 빌드해야하므로 시간을 낭비하게 됨.
* 의존성 설치 명령
```bash
rosdep install -i --from-path src --rosdistro foxy -y
```

* 결과
```
#All required rosdeps installed successfully
```

* 원리
  * package.xml 파일에 선언된 의존성을 보고 설치되어 있지 않으면 설치하는 방식


### 2-5 colon으로 workspace 빌드하기
* ros2_ws 디렉토리에서 아래 아래 명령으로 빌드하기
```bash
colcon build
```

* 결과
```
Starting >>> turtlesim
Finished <<< turtlesim [5.49s]

Summary: 1 package finished [5.58s]
```

* 빌드 결과물 확인
```bash
cd ~/ros2_ws
ls
```

* 결과
```
build  install  log  src
```
  * install 디렉토리에 setup 파일이 위치한다. (overlay 환경 설정)

### 2-6 overlay source
* 빌드 후에 새 터미널에서 빌드한 workspace에 대해서 환경설정(overlay source)
* ROS 2 환경을 source (underlay)
```
source /opt/ros/foxy/setup.bash
```

* workspace로 이동
```bash
cd ~/ros2_ws
```

* overlay에 대한 source
```bash
source install/local_setup.bash
```

* overlay 설정 후 turtlesim package 실행하기
```
ros2 run turtlesim turtlesim_node
```

* underlay turtlesim vs. overlay turtlesim
  * 확인 방법은?

### 2-7 overlay 수정하기
* turtlesim 소스 수정하기
  * ~/ros2_ws/src/ros_tutorials/turtlesim/src/turtle_frame.cpp 파일 열기
  * 52번째 줄 수정
    * "TurtleSim"을 "MyTurtleSim"으로 수정

* 첫번째 터미널로 이동하여 아래 실행
```bash
cd ~/ros2_ws
colcon build
```

* 2번째 터미널에서 turtlesim 실행하기
```bash
ros2 run turtlesim turtlesim_node
```

* 결과

![](https://docs.ros.org/en/foxy/_images/overlay.png)

  * "MyTurtleSim" 타이틀 확인하기

* 새로운 터미널 열어서 실행해보기 (underlay turtlesim 확인하기)
```bash
ros2 run turtlesim turtlesim_node
```

* 결과
![](https://docs.ros.org/en/foxy/_images/underlay.png)
