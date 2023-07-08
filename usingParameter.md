# parameter 사용하기 (C++)
1. 개요
2. 실습

## 1. 개요
* ROS parameter를 사용하기
* node를 작성할때 해당 node에서 필요한 parameters가 필요한 경우가 있다. 

## 2. 실습
### 2-1 package 생성하기


### 2-1-1 package.xml 업데이트하기

### 2-2 C++ node 작성하기

### 2-2-1 실행자(executable) 추가하기

### 2-3 빌드 및 실행하기
* 의존성 확인하는 명령 실행
```bash
rosdep install -i --from-path src --rosdistro foxy -y
```
* 새 package를 빌드하기
```bash
cd ~/ros2_ws
colcon build --packages-select cpp_parameters
```

* 새 터미널 열고 source 하기
```bash
source install/setup.bash
```

* node 실행하기
```bash
ros2 run cpp_parameters minimal_param_node
```
* 결과
```
[INFO] [minimal_param_node]: Hello world!
```

### 2-3-1 console로 변경하기
* node 실행하기
```bash
ros2 run cpp_parameters minimal_param_node
```
* 새 터미널 열고 source 실행한 후에 아래 명령 실행

```bash
ros2 param list
```

* my_parameter 설정하기
```bash
ros2 param set /minimal_param_node my_parameter earth
```

* 결과
```
Set parameter successful
```

* 새 터미널에서 source 후 아래 명령 실행해보기
```bash
ros2 run cpp_parameters minimal_param_node
```

* 결과
```
[INFO] [minimal_param_node]: Hello earth!
```

### 2-3-2 launch 파일로 변경하기
* ros2_ws/src/cpp_parameters/ 디렉토리 내부에 launch 디렉토리 생성
* launch 디렉토리 내부에 cpp_parameters_launch.py 파일 (아래 내용 붙여넣기)
```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package="cpp_parameters",
            executable="minimal_param_node",
            name="custom_minimal_param_node",
            output="screen",
            emulate_tty=True,
            parameters=[
                {"my_parameter": "earth"}
            ]
        )
    ])
```

* CMakeLists.txt 파일에 아래 코드 추가하기
```cmake
install(
  DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
```

* 빌드하기
```bash
colcon build --packages-select cpp_parameters
```

* 새 터미널에서 source 하기
```bash
source install/setup.bash
```

* node 실행하기
```bash
ros2 launch cpp_parameters cpp_parameters_launch.py
```

* 결과
```
[INFO] [custom_minimal_param_node]: Hello earth!
```

