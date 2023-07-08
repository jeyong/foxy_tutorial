# action 이해
1. 소개
2. 실습

## 1. 개요
* 
![](https://docs.ros.org/en/foxy/_images/Action-SingleActionClient.gif)

## 2. 실습
### 2-1 설정
* 2개 nodes 실행 : /turtlesim, /teleop_turtle
* 새 터미널에서 실행
```bash
ros2 run turtlesim turtlesim_node
```

* 새 터미널에서 실행
```bash
ros2 run turtlesim turtle_teleop_key
```

### 2-2 action 사용하기
* /teleop_turtle node 실행 화면
```
Use arrow keys to move the turtle.
Use G|B|V|C|D|E|R|T keys to rotate to absolute orientations. 'F' to cancel a rotation.
```
* 
```
[INFO] [turtlesim]: Rotation goal completed successfully
```


```
[INFO] [turtlesim]: Rotation goal canceled
```

```
[WARN] [turtlesim]: Rotation goal received before a previous goal finished. Aborting previous goal
```

### 2-3 ros2 node info
* /turtlesim 
```bash
ros2 node info /turtlesim
```

* 결과
```
/turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Services:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:
```

* /teleop_turtle node 정보 보기 명령
```bash
ros2 node info /teleop_turtle
```
* 결과
```
/teleop_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Services:
    /teleop_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /teleop_turtle/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /teleop_turtle/get_parameters: rcl_interfaces/srv/GetParameters
    /teleop_turtle/list_parameters: rcl_interfaces/srv/ListParameters
    /teleop_turtle/set_parameters: rcl_interfaces/srv/SetParameters
    /teleop_turtle/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Action Servers:

  Action Clients:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
```

### 2-4 ros2 action list
* ROS graph내에서 모든 actions 보기 명령
```bash
ros2 action list
```

* 결과
```
/turtle1/rotate_absolute
```

### 2-4-1 ros2 action list -t
* action의 type 보기 (/turtle1/rotate_absolute의 type보기)
```bash
ros2 action list -t
```

* 결과(/turtle1/rotate_absolute의 type보기)
```
/turtle1/rotate_absolute [turtlesim/action/RotateAbsolute]
```
  * action type : turtlesim/action/RotateAbsolute


### 2-5 ros2 action info
* /turtle1/rotate_absolute action에 대한 상세 정보 보기 명령
```bash
ros2 action info /turtle1/rotate_absolute
```

* 결과
```
Action: /turtle1/rotate_absolute
Action clients: 1
    /teleop_turtle
Action servers: 1
    /turtlesim
```
  * /teleop_turtle node : action client
  * /turtlesim node : action server

### 2-6 ros2 interface show
* action을 보내거나 실행하기 위해서 상세 정보가 필요
* /turtle1/rotate_absolute 의 action type인 turtlesim/action/RotateAbsolute 의 상세 정보 보기 명령
```bash
ros2 interface show turtlesim/action/RotateAbsolute
```
* 결과
```
# The desired heading in radians
float32 theta
---
# The angular displacement in radians to the starting position
float32 delta
---
# The remaining rotation in radians
float32 remaining
```

### 2-7 ros2 action send_goal
* 
```bash
ros2 action send_goal <action_name> <action_type> <values>
```

* 
```bash
ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"
```

* 결과
```
Waiting for an action server to become available...
Sending goal:
   theta: 1.57

Goal accepted with ID: f8db8f44410849eaa93d3feb747dd444

Result:
  delta: -1.568000316619873

Goal finished with status: SUCCEEDED
```

```bash
ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: -1.57}" --feedback
```

* 결과
```
Sending goal:
   theta: -1.57

Goal accepted with ID: e6092c831f994afda92f0086f220da27

Feedback:
  remaining: -3.1268222332000732

Feedback:
  remaining: -3.1108222007751465

…

Result:
  delta: 3.1200008392333984

Goal finished with status: SUCCEEDED
```