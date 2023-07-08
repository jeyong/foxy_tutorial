# node 실행하기
1. 개요
2. 실습

## 1. 개요
* 

## 2. 실습
### 2-1 launch 파일 실행시키기
* 새 터미널에서 실행하기
```bash
ros2 launch turtlesim multisim.launch.py
```

* multisim.launch.py 파일 내부
```python
# turtlesim/launch/multisim.launch.py

from launch import LaunchDescription
import launch_ros.actions

def generate_launch_description():
    return LaunchDescription([
        launch_ros.actions.Node(
            namespace= "turtlesim1", package='turtlesim', executable='turtlesim_node', output='screen'),
        launch_ros.actions.Node(
            namespace= "turtlesim2", package='turtlesim', executable='turtlesim_node', output='screen'),
    ])
```

![](https://docs.ros.org/en/foxy/_images/turtlesim_multisim.png)


