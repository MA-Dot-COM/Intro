# <img src="https://user-images.githubusercontent.com/111809392/205326221-6542a55f-fae2-4ece-982f-0b9598f4f08c.png" height="50"/>  SorHive 프로젝트 

## 공간을 통해 일상을 연결하는 플랫폼
<img src="https://user-images.githubusercontent.com/111809392/205321871-c7de56fd-34cc-4a74-9f22-189ec16f87fe.png" height="300"/>

# Contents
- [Development-Record](https://github.com/MA-Dot-COM/Intro/wiki/Development-Record)
- [참고자료](https://github.com/MA-Dot-COM/Intro/wiki/%EC%B0%B8%EA%B3%A0-%EC%9E%90%EB%A3%8C)

# 주요기능
- 자신의 일상을 담을 수 있는 페이지
<div>
<img src="https://user-images.githubusercontent.com/111809392/205321857-2650fe08-b253-495b-8477-f8120b5522fd.png" width="45%"/>
<img src="https://user-images.githubusercontent.com/111809392/205321864-1b3b4ccf-4be0-4acd-b671-36a8478f0166.png" width="45%"/>
<div/>
  
# Built With

<details>
<summary>Unity(XR) 기술과 사용 이유</summary>
<div markdown="1">

- [Unity Enterprise](https://store.unity.com/kr/products/unity-enterprise)
  - 전체 UI 및 3D공간
- [Photon](https://www.photonengine.com/ko-KR/)
  - 다중사용자 환경
- [Blender](https://www.blender.org/)
  - 아바타 및 프리셋

</div>
</details>

<details>
<summary>AI 기술과 사용 이유</summary>
<div markdown="1">

- [Tensorflow](https://www.tensorflow.org/?hl=ko)
  -
- [Pytorch](https://pytorch.org/)
  -
- [Pycharm](https://www.jetbrains.com/ko-kr/pycharm/)
  -
- [Fastapi](https://fastapi.tiangolo.com/ko/)
  -
- [Docker](https://www.docker.com/)
  -

--------

 - 공간 분류모델
네이버, 구글에서 술집, 노래방, 카페등 공간에 대한 이미지 크롤링후 전처리, 약 12,000개의 데이터셋을 Resnet50모델에 전이학습하여 사용자가 일상의 사진을 올리면 분석하여 그와 맞는 공간에 대한 카테고리를 분류해 준다. 

- 아바타 생성모델
사용자의 얼굴 사진으로 아바타를 생성해주는 시스템을 설계하고 구현, 데이터 셋은 https://www.kaggle.com/datasets/niten19/face-shape-dataset를 사용한다. 얼굴이 이미 나누어져 있는 kaggle의 Face Shape Dataset 중 약 2500개를 사용해 눈모양과 눈썹모양을 라벨링 한 후, yolo5로 학습시켰다. yolo5의 detect.py와 data.yaml 수정해 얼굴형, 눈모양, 눈썹모양 별로 모델을 만든 뒤, 각 클래스마다 높은 값을 뽑아내 사용자의 얼굴사진을 분석해 아바타를 만든다. 

- Insightface의 Detection모델
공간분류 모델에 사용될 사용자들의 이미지 데이터의 초상권 보호를 위해 Insightface의 Detection모델인 RetinaFace-10GF를 사용하여 얼굴인식 후 모자이크 처리를 해주는 모델을 만들었다. 모자이크 처리한 데이터셋으로 공간분류 모델을 학습한 결과 성능의 차이는 없었고, 이후에도 사용자들에게 사진을 받으면 Insightface의 Detection모델을 거쳐 모자이크 처리되어 초상권이 보호된 데이터셋으로 활용할 계획이다.

- 추천 시스템
사용자 기반 협업 필터링을 통해 사용자 간 친밀도를 측정해 잠재적인 관계가 가깝지만 아직 팔로워 하지 않은 사용자를 추천해 주는 시스템을 설계하고 구현.
친구 친밀도 도출 시스템은 사용자에게 얼마나 관심이 많은지 클릭해서 본 빈도(룸인, 라이핑, 채팅 등)등 사용자 행동 양식을 수집하여 얼마나 친밀한지 판별하고,
이를 토대로 사용자에 대해 친밀도 순위를 결정한다.

</div>
</details>

<details>
<summary>Backend(NET) 기술과 사용 이유</summary>
<div markdown="1">

- [AWS RDS - MySQL](https://aws.amazon.com/ko/rds/mysql/?nc=sn&loc=1)
  - 정규화를 통해 데이터의 일관성과 무결성을 확보하기 위해 사용했습니다.

- [MongoDB - Atlas](https://www.mongodb.com/ko-kr/cloud/atlas/efficiency)
  - 방대한 데이터 처리, 수정 필요없는 데이터들만 저장하여 빠르게 조회가 가능해서 사용했습니다.
  
- [AWS Ec2](https://aws.amazon.com/ko/ec2/)
  - 클라우드 환경의 가상 서버를 구축하기 위해 사용했습니다.
  
- [AWS S3](https://aws.amazon.com/ko/s3/?nc=sn&loc=0)
  - 이미지 저장, 호스팅, 뛰어난 보안성 때문에 사용했습니다.
  
- [AWS ElasticBeanstalk](https://aws.amazon.com/ko/elasticbeanstalk/)
  - 서버에서 개발된 웹 애플리케이션 및 서비스를 간단하게 배포하려고 사용한 서비스
  - 로드밸런싱, 오토스케일링 기능 함께 사용했습니다.

- [AWS Route53](https://aws.amazon.com/ko/route53)
  - ACM 과 ElasticBeanstalk 를 연결하여 사용했습니다.
  - Domain은 sorhive.shop 을 통해 접속 가능하게 하였습니다.

- [AWS Certificate Manager](https://aws.amazon.com/ko/certificate-manager)
  - 로드밸런서에 SSL 인증서를 연결하여 사용했습니다.
  - HTTP에 SSL 인증서를 사용하여 더 안전한 보안용 프로토콜인 HTTPS를 통해 더 안전한 SNS를 위해 사용했습니다.

- [SpringBoot](https://spring.io/projects/spring-boot)
  - 자바 기반의 웹 어플리케이션을 만들 수 있는 프레임워크인 스프링을 더 쉽게 사용할 수 있어서 사용했습니다.
  
- [JPA](https://spring.io/projects/spring-data-jpa)
  - 객체와 관계형 데이터베이스를 매핑하여 데이터베이스에 대한 의존성을 줄이고 생산성을 높이고 유지보수 향상, 성능 등의 장점 때문에 사용했습니다. 
  
- [Spring Security](https://spring.io/projects/spring-security)
  - 스프링 어플리케이션의 보안을 담당하는 스프링 하위 프레임 워크이고, 인증과 권한 부분을 담당했습니다.
  - JsonWebToken과 함께 사용하여 토큰 기반으로 접근을 통제했습니다.
  
- [Spring Batch](https://spring.io/projects/spring-batch)
  - 스프링 어플리케이션에서 일괄적인 데이터 처리를 담당하는 스프링 하위 프레임워크이고,
  - 라이핑(스토리)의 특성인 24시간 이후 안보이게 하는 기능
  - 추천배열(AI에 회원 * 회원에 대한 데이터를 통해 받아온 코사인 유사도 기반 추천 정렬)을 받아오고 몽고 DB에 저장하는 기능
    2 가지를 위해서 사용했습니다.
    
--------

- 회원 접근 권한 및 토큰 발급 : Spring Security, jsonwebtoken
- 데이터 일괄 처리 : Spring-Batch
- Object-relational mapping : jpa
- 이메일 처리 : Spring-Boot-Starter-Mail
- 로드밸런싱 : AWS Elastic Load Balancing, AWS Route53, AWS ACM
- 데이터 저장 : RDS
- 대량 데이터 저장 : MongoDB
- 파일 저장 : AWS S3

---------

</div>
</details>

# MLOps
<details>
<summary>MLOps</summary>
<div markdown="1">
 
## 이미지 → image classification → 공간

(사진)XR → NET → AI(분석) → NET → (공간)XR
  
<div>
  
<img src="https://user-images.githubusercontent.com/111809392/205317427-cd9e6372-9368-4d9f-86f3-41c7adfb881a.png" width="30%" height="400"/>
<img src="https://user-images.githubusercontent.com/111809392/205317453-a6147b69-ae54-4fe6-8818-6be44fe28bdb.png" width="30%" height="400"/>
<img src="https://user-images.githubusercontent.com/111809392/205317463-7ec76e89-f5ce-44f7-a955-9a8bd252d188.png" width="30%" height="400"/>
                                                                                                                            
<div/>
                                                                                                                            
![Untitled (1)](https://user-images.githubusercontent.com/111809392/205317472-345c07bd-c83f-4098-a359-9cb7f0870ba7.png)
![Untitled](https://user-images.githubusercontent.com/111809392/205317480-bf87aa5b-7f5a-43e6-b19e-9a27e770ef69.png)
  
</div>
</details>
 
# 테스트
<details>
<summary>Android 디버그 브리지(ADB)의 vmstat 출력값 이용 결과</summary>
<div markdown="1">
 

  - 실제 사용하던 폰으로 해서 튀는 부분이 일부 존재 한다.
  - 백그라운드 앱 종료 후 10분간 대기
  - 이후 앱 구동 & 로그인 후 50분 대기
  - 이후 앱 종료 후 10분간 대기 한 그래프
![성능테스트](https://user-images.githubusercontent.com/111809392/205322590-ef6e49ac-3ad7-4bf9-b79a-7828c62a066e.png)
![성능테스트2](https://user-images.githubusercontent.com/111809392/205322666-1fe6c65c-4f7a-4339-a374-531bd9e1d0b9.png)
  
</div>
</details>
  

<details>
<summary>Jmeter 이용 3만건 가량의 POST 테스트 결과</summary>
<div markdown="1">
 
- AWS Cloud Watch 그래프
![부하테스트 결과](https://user-images.githubusercontent.com/111809392/205322686-4f8fb92a-7c86-4572-8899-583ca1d0908d.png)
![부하테스트 결과2](https://user-images.githubusercontent.com/111809392/205322699-3fe3e45c-3ce7-4622-9865-3f7d07a657b4.png)

</div>
</details>

# 융합 구조도
![융합구조도](https://user-images.githubusercontent.com/111809392/205318829-a7071a0d-5c43-4265-b92b-1fedc3d0e5b2.png)

# Author
- 박찬영(AI) - [GitHub](https://github.com/orgs/MA-Dot-COM/people/Jneck)
- 이성빈(AI) - [GitHub](https://github.com/orgs/MA-Dot-COM/people/naya-beene)
- 최나영(AI) - [GitHub](https://github.com/orgs/MA-Dot-COM/people/cny689)
- 부시연(Backend) - [Github](https://github.com/SybooSyboo782)
- 신정훈(Unity) - [GitHub](https://github.com/orgs/MA-Dot-COM/people/JasonShin10)
- 이현영(Unity) - [GitHub](https://github.com/orgs/MA-Dot-COM/people/leeHY22)
