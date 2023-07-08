# parameter 이해
1. 개요
2. 실습

## 1. 개요
* 
## 2. 실습
### 2-1 설정
* 2개 node 구동시키기 : /turtlesim ,  /teleop_turtle 

* turtlesim_node node 실행
```bash
ros2 run turtlesim turtlesim_node
```

* turtle_teleop_key node 실행
```bash
ros2 run turtlesim turtle_teleop_key
```

### 2-2 ros2 param list
* 해당 nodes에 속해있는 parameters 확인하기
```
ros2 param list
```

* 2개 nodes에 속하는 parameters 보기
```
/teleop_turtle:
  scale_angular
  scale_linear
  use_sim_time
/turtlesim:
  background_b
  background_g
  background_r
  use_sim_time
```

### 2-3 ros2 param get
* parameter의 type과 현재 값 표시
```bash
ros2 param get <node_name> <parameter_name>
```
* /turtlesim의 background_g parameter 값 표시
```bash
ros2 param get /turtlesim background_g
```
* 결과
```bash
Integer value is: 86
```
### 2-4 ros2 param set
* 실시간으로 현재 parameter 값 변경하는 명령
```bash
ros2 param set <node_name> <parameter_name> <value>
```
* /turtlesim 의 배경색 변경해보기
```bash
ros2 param set /turtlesim background_r 150
```

* 결과
```
Set parameter successful
```

![](https://docs.ros.org/en/foxy/_images/set.png)

### 2-5 ros2 param dump
* 
```bash

```

### 2-6 ros2 param load
* 현재 실행 중인 node의 parameter를 load하기
```bash
ros2 param load <node_name> <parameter_file>
```
* 
### 2-7 node 시작시킬때 parameter 파일을 로드시키기
* 
```bash

```


```bash

```
