# 1차 AI Aris 시연 영상 및 부가 설명


최근 LLM 과 더불어 RAG 기술로 도메인에 관한 대화능력을 강화시킬 수 있는 방안이 생겼음에 따라 aris 라는 아이스크림 제조 로봇에 사람과 같이 대화로 고객의 주문을 접수받는 ai 접수원을 만들었습니다. 기존에는 키오스크로 입력을 주문 받아 키오스크에 친숙하지 않거나 사용법을 잘 모르는 분들은 불편함을 느끼거나, 주문을 받는데 오랜 시간이 소요되어 뒤에 대기 시간이 늘어나는 단점이 있었습니다. 저희 ai 아이스크림 접수원은 다음과 같은 점을 통해 이러한 단점을 극복하고 사람에게 더 친숙함을 제공하였습니다.
1. 고객이 오면 카메라로 고객의 얼굴을 인식하여 회원인지, 처음 방문하신 분인지 판별합니다.
2. 회원이시면 스스로 방문횟수를 체크하고 적립합니다. 또한 회원이 이전에 주문한 이력을 기억했다가 이야기를 통해 주문한 이력을 고객이 알 수가 있습니다.
3. AI 접수원이 대화로 아이스크림 주문을 접수하면 aris 아이스크림 제조 로봇과 연동되어 로봇이 바로 아이스크림을 만들어 줍니다.
아래는 이런 서비스 기술을 구현한 주요 과정 및 정보를 기록했습니다.
## 구현 못했던 기술들

## 시연 영상

[![Video Label](http://img.youtube.com/vi/OnH8ScQYvCw/0.jpg)](https://www.youtube.com/watch?v=OnH8ScQYvCw)

## 주요 기술 구성요소
1. Large Language Model (LLM) + Retrieval-Augmented Generation (RAG)
2. FastAPI 서버 (UI 화면-백엔드 연동)
3. DB: 고객 얼굴 및 데이터 관리
4. Face Recognition
5. Object Detection
6. Robot Motion

## 프로젝트 팀 구성
|이름|역할|
|--|--|
|김현우|Rag pipeline 구축, llm finetuning, fastapi 서버 구축, face recogntion|
|김태현|db 구축, face recognition, stt|
|라환철|llm finetuning, fastapi 서버 통합, stt|
|박성우|로봇 모션 제어 , 로봇 모션 로직 구현, Object Detection|
|이지헌|로봇 모션 제어, 로봇 모션 로직 구현, 아루코 마커|

## 배운 점

|이름|깨달은 점|
|--|--|
|김현우|-|
|김태현|-|
|라환철||- llm 을 일반 컴퓨터에서 돌리려면 quantization이 중요하다는 것. - llm 을 finetuning 시 custom 데이터를 특정상황을 잘 구분지어 다양한 질문-대답 set를 만들어야 된다는 것.
- stt 모델이 한국어 모델이 많이 컸기에 인터넷이 안되는 로컬 노트북 환경에서는 잘 인식이 안되어서 인터넷과 동시에 로봇을 연결하는 것이 중요하다는 것.  또한 한국어 모델이 quantized 하면 많이 성능이 안좋아진다는 것.
- 각각의 기능을 구현할 때는 잘 작동했지만, 이것을 한번에 동작시키는 것에서 많은 난관이 있다는 것( 돌아가는 환경 충돌, 실시간 동작 구현 , 기능을 추가할 때마다 기존 코드 어디를 손봐야할 지 등등 )
- 로봇을 실험할 때 실제 환경에서 코드를 실험하는 것은 매우 위험할 수도 있다는 것과, 로봇 시뮬레이션 환경이 중요하다는 것.
여러 사람이 짠 코드를 통합시킬 때 , 혹은 새로 개선된 코드를 통합 코드에 다시 통합시킬 때 그 사람과의 소통하는 능력, 코드와 코드를 잇는 연결 과정이 어렵다는 것 등을 배웠음.|
|박성우|-|
|이지헌|-|

### 1. 문제 해결 접근법
- 오류를 만났을 때 최소 30분 정도는 스스로 해결하려고 노력해야 했습니다.
  - 이를 통해 문제에 대한 이해도를 높이고, 해결한 경우 다른 사람들에게 설명하기 쉬우며, 비슷한 문제가 다시 발생했을 때 스스로 해결할 수 있었습니다.

### 2. 시뮬레이션의 중요성
- 로봇 작업 시, 실제 환경에서 테스트하기 전에 시뮬레이션을 통해 경로와 동작을 점검하는 것이 중요하다.
- 잘못된 경로 설정은 로봇 충돌 등의 위험을 초래할 수 있습니다.

### 3. 개발자 노트의 중요성
- 오류, 명령어, 해결 방법 등을 체계적으로 기록해두면 문제 해결 속도가 크게 향상되었습다.
- 팀원들과 이러한 노트를 공유하면 협업의 효율이 배가됐습니다.

llm 을 일반 컴퓨터에서 돌리려면 quantization이 중요하다는 것.
llm 을 finetuning 시 custom 데이터를 특정상황을 잘 구분지어 다양한 질문-대답 set를 만들어야 된다는 것.
stt 모델이 한국어 모델이 많이 컸기에 인터넷이 안되는 로컬 노트북 환경에서는 잘 인식이 안되어서 인터넷과 동시에 로봇을 연결하는 것이 중요하다는 것.  또한 한국어 모델이 quantized 하면 많이 성능이 안좋아진다는 것.
각각의 기능을 구현할 때는 잘 작동했지만, 이것을 한번에 동작시키는 것에서 많은 난관이 있다는 것( 돌아가는 환경 충돌, 실시간 동작 구현 , 기능을 추가할 때마다 기존 코드 어디를 손봐야할 지 등등 )
7:16
로봇을 실험할 때 실제 환경에서 코드를 실험하는 것은 매우 위험할 수도 있다는 것과, 로봇 시뮬레이션 환경이 중요하다는 것.
여러 사람이 짠 코드를 통합시킬 때 , 혹은 새로 개선된 코드를 통합 코드에 다시 통합시킬 때 그 사람과의 소통하는 능력, 코드와 코드를 잇는 연결 과정이 어렵다는 것 등을 배웠음

---

## 문제 해결

### 픽업존 센서 문제
- **상황**: 프로젝트 진행 중 픽업존 센서를 사용할 수 없었습니다.
  - ARIS 시스템에서는 픽업존 센서가 컵이 놓인 위치를 자동으로 로봇에 전달하지만, 이 프로젝트에서는 센서 사용이 금지되었습다.
- **해결 방법**: 객체 인식 기술을 도입하여 컵의 위치를 감지하는 방식으로 문제를 해결했습니다. 먼저 boundary box를 설정한뒤, 컵이 그안에 3초동안 머물러 있으면 컵이 놓여졌다는것을 인식하고 프로그램은 컵의 위치를 입력값으로 받습니다.

- **상황2**: 사진 자료들을 수집할때 컵과 손이 같이 있는 경우도 학습을 시켜서, 손이 없으면 컵을 인식을 못하는 상황이 있었습니다. 

- **해결 방법** 컵만 있는 사진들을 수집해서 재학습을 시켰는데 손이 없는데도 컵을 confidence level이 94% 이상 나올 정도로 높은 정확도를 구현해 낼수 있었습니다.



-아쉬운 점
 - 당연하게도 시간이 많이 없었다. 계속해서 계획을 수정하고
 - 

