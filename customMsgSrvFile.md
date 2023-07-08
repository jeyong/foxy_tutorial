# 커스텀 msg와 srv 파일 생성하기
1. 소개
2. 실습

## 1. 소개
* 사용자가 원하는 .msg와 .svr 파일 정의하기

## 2. 실습
### 2-1 새 package 생성하기
* 생성한 .msg와 .srv 파일을 사용하는 package 생성

* 새로운 package 생성
```bash
ros2 pkg create --build-type ament_cmake tutorial_interfaces
```

* .msg와 .srv 파일은 각각 msg와 srv 디렉토리 내에 위치한다.
* ros2_ws/src/tutorial_interfaces 내에 아래 명령 수행
```bash
mkdir msg srv
```

### 2-2 커스텀 정의 생성하기

### 2-2-1 msg 정의
* tutorial_interfaces/msg 디렉토리 내부에 Num.msg 파일 생성하기
* Num.msg 파일 내부
```
int64 num
```

* tutorial_interfaces/msg 디렉토리 내부에 Sphere.msg 파일 생성하기
* Sphere.smg 파일 내부
```
geometry_msgs/Point center
float64 radius
```
  * 다른 message package에 있는 message를 사용 

### 2-2-2 srv 정의
* tutorial_interfaces/msg 디렉토리 내부에 AddThreeInts.srv 파일 생성하기
* AddThreeInts.srv 파일 내부
```
int64 a
int64 b
int64 c
---
int64 sum
```

### 2-3 CMakeLists.txt 
```cmake
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Sphere.msg"
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)
```

### 2-4 package.xml
* package.xml 내에 <package> element 내부에 아래 코드를 추가
```xml
<depend>geometry_msgs</depend>
<buildtool_depend>rosidl_default_generators</buildtool_depend>
<exec_depend>rosidl_default_runtime</exec_depend>
<member_of_group>rosidl_interface_packages</member_of_group>
```

### 2-5 tutorial_interfaces package 빌드하기
```bash
colcon build --packages-select tutorial_interfaces
```

### 2-6 msg와 srv 생성 확인
* source 실행
```bash
source install/setup.bash
```

* ros2 interface show 명령으로 확인하기
```bash
ros2 interface show tutorial_interfaces/msg/Num
```

* 결과
```
int64 num
```

* ros2 interface show 명령으로 확인하기
```bash
ros2 interface show tutorial_interfaces/msg/Sphere
```

* 결과
```
geometry_msgs/Point center
        float64 x
        float64 y
        float64 z
float64 radius
```

* ros2 interface show 명령으로 확인하기
```bash
ros2 interface show tutorial_interfaces/srv/AddThreeInts
```

* 결과
```
int64 a
int64 b
int64 c
---
int64 sum
```

### 2-7 새로운 interface 테스트
* 