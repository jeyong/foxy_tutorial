# topic 이해
1. 개요
2. 실습

## 1. 개요
* rqt_graph와 CLI 도구사용해서 ROS 2 topics 알아보기
  * ROS 2에서는 시스템은 모듈화된 여러 nodes로 구성
  * topics = bus 
  * 각 node가 data를 교환하는 bus
![](https://docs.ros.org/en/foxy/_images/Topic-SinglePublisherandSingleSubscriber.gif)

  * node는 여러 data를 동시에 publish/subscribe가 가능하다.
![](https://docs.ros.org/en/foxy/_images/Topic-MultiplePublisherandMultipleSubscriber.gif)

  * nodes 사이에 data를 이동시키는 가장 일반적인 방법

## 2. 실습
