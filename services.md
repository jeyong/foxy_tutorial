# service 이해
1. 개요
2. 실습

## 1. 개요
* ROS graph 상에서 nodes 사이에서의 통신 방법 
* publisher-subscriber 모델 vs. call-and-response 모델
* topics : publisher가 지속적으로 data stream 을 subscriber에게 제공
* services : client가 요청하면 그 요청에 따라서 server가 data를 제공

![](https://docs.ros.org/en/foxy/_images/Service-SingleServiceClient.gif)

* 동작 이해하기

![](https://docs.ros.org/en/foxy/_images/Service-MultipleServiceClient.gif)

## 2. 실습
### 2-1 환경설정
* 2가지 turtlesim nodes 구동시키기
  * /turtlesim
  * /teleop_turtle
* 새 터미널 열고 실행
```bash
ros2 run turtlesim turtlesim_node
```
* 새 터미널 열고 실행
```bash
ros2 run turtlesim turtle_teleop_key
```

## 2-2 ros2 service list
* ros2 service list 명령 실행
```bash
ros2 service list
```

* 결과
```
/clear
/kill
/reset
/spawn
/teleop_turtle/describe_parameters
/teleop_turtle/get_parameter_types
/teleop_turtle/get_parameters
/teleop_turtle/list_parameters
/teleop_turtle/set_parameters
/teleop_turtle/set_parameters_atomically
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative
/turtlesim/describe_parameters
/turtlesim/get_parameter_types
/turtlesim/get_parameters
/turtlesim/list_parameters
/turtlesim/set_parameters
/turtlesim/set_parameters_atomically
```

* 현재 활성화되어 있는 모든 services을 표시

* 집중적으로 볼 services
  * /clear
  * /kill
  * /reset
  * /spawn
  * /turtle1/set_pen
  * /turtle1/teleport_absolute
  * /turtle1/teleport_relative

* 이전에 rqt를 이용해서 몇 가지 services에 대해서는 다뤄봤다.

### 2-3 ros2 service type
* service type이란
  * topic type과 유사
  * service의 request와 response data 구조
  * 2개 부분으로 구성 : request, response 
* service type 확인하는 명령
```bash
ros2 service type <service_name>
```

* /clear service type 확인해보기
```bash
ros2 service type /clear
```
* 결과
```bash
std_srvs/srv/Empty
```
  * Empty type은 request와 response로 어떤 data를 보내거나 받는 않는 type

### 2-3-1 ros2 service list -t
* 활성화된 services 목록과 그 types 확인하기
```bash
ros2 service list -t
```
  * 옵션 : --show-types 혹은 -t 

* 결과
```
/clear [std_srvs/srv/Empty]
/kill [turtlesim/srv/Kill]
/reset [std_srvs/srv/Empty]
/spawn [turtlesim/srv/Spawn]
...
/turtle1/set_pen [turtlesim/srv/SetPen]
/turtle1/teleport_absolute [turtlesim/srv/TeleportAbsolute]
/turtle1/teleport_relative [turtlesim/srv/TeleportRelative]
...
```

### 2-4 ros2 service find
* 특정 type을 가지는 모든 services 목록 확인하는 명령
```
ros2 service find <type_name>
```

* Empty 타입의 services 목록
```bash
ros2 service find std_srvs/srv/Empty
```
* 결과
```
/clear
/reset
```

### 2-5 ros2 interface show
* 

### 2-6 ros2 service call
* 터미널에서 services 직적 호출하려면 해당 service의 내부 구조를 알아야 값을 입력할 수 있다.
* service의 구조 보기 명령
```bash
ros2 interface show <type_name>.srv
```
* /clear service type에 대해서 실행
```bash
ros2 interface show std_srvs/srv/Empty.srv
```
* 결과 ((Empty type)
```
---
```
  * --- 은 request와 response를 구분해주는 구분자. Empty type의 경우 data를 주고 받는 것이 없으므로 공백으로 표현

* /spawn service의 request/response 보는 명령
```bash
ros2 interface show turtlesim/srv/Spawn
```
* 결과
```bash
float32 x
float32 y
float32 theta
string name # Optional.  A unique name will be created and returned if this is empty
---
string name
```
  * spawn시키기 위해서 x, y, theta -> 생성할 turtle의 2D pose
  * name은 option

### 2-6 ros2 service call
* service type을 알게 되었으니 이를 이용해서 service 호출하기
```bash
ros2 service call <service_name> <service_type> <arguments>
```
  * <arguments> 부분은 옵션. Empty type을 가지는 service는 arguments가 필요없음

* /clear service 호출해보기
```bash
ros2 service call /clear std_srvs/srv/Empty
```
* 결과

![](https://docs.ros.org/en/foxy/_images/clear.png)
  * turtlesim 창을 clear하는 명령

* /spawn service 호출하기 (YAML 문법 사용)
```bash
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"
```

* 결과
```bash
requester: making request: turtlesim.srv.Spawn_Request(x=2.0, y=2.0, theta=0.2, name='')

response:
turtlesim.srv.Spawn_Response(name='turtle2')
```

![](https://docs.ros.org/en/foxy/_images/spawn1.png)
