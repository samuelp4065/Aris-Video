# 1차 AI Aris 시연 영상 및 부가 설명

최근 LLM과 더불어 RAG 기술로 도메인에 관한 대화 능력을 강화할 수 있는 방안이 생기면서, Aris라는 아이스크림 제조 로봇에 사람과 대화로 고객의 주문을 접수받는 AI 접수원을 개발했습니다. 기존에는 키오스크로 주문을 받았으나, 키오스크에 친숙하지 않거나 사용법을 잘 모르는 분들은 불편함을 느끼거나 주문 시간이 길어져 대기 시간이 늘어나는 단점이 있었습니다. 저희 AI 아이스크림 접수원은 다음과 같은 점에서 이러한 단점을 극복하고 사람에게 더 친숙한 경험을 제공합니다.

1. **고객 인식 및 판별**: 카메라를 통해 고객 얼굴을 인식하여 회원인지, 처음 방문한 분인지 판별합니다.
2. **회원 관리 및 주문 이력**: 회원이라면 방문 횟수를 자동으로 체크하고 적립합니다. 또한, 이전 주문 이력을 기억하여 대화를 통해 고객이 이전 주문을 쉽게 알 수 있습니다.
3. **AI 접수 및 연동**: AI 접수원이 대화로 주문을 접수하면 Aris 아이스크림 제조 로봇과 연동되어 로봇이 바로 아이스크림을 제작합니다.

## 시연 영상

[![Video Label](http://img.youtube.com/vi/OnH8ScQYvCw/0.jpg)](https://www.youtube.com/watch?v=OnH8ScQYvCw)

---

## 주요 기술 구성 요소

1. **Large Language Model (LLM) + Retrieval-Augmented Generation (RAG)**
2. **FastAPI 서버**: UI 화면-백엔드 연동
3. **데이터베이스 (DB)**: 고객 얼굴 및 데이터 관리
4. **Face Recognition**
5. **Object Detection**
6. **Robot Motion**

---

## 프로젝트 팀 구성

| 이름   | 역할                                                   |
|--------|--------------------------------------------------------|
| 김현우 | RAG 파이프라인 구축, LLM 파인튜닝, FastAPI 서버 구축, Face Recognition |
| 김태현 | DB 구축, Face Recognition, STT                       |
| 라환철 | LLM 파인튜닝, FastAPI 서버 통합, STT                  |
| 박성우 | 로봇 모션 제어, 로봇 모션 로직 구현, Object Detection  |
| 이지헌 | 로봇 모션 제어, 로봇 모션 로직 구현, 아루코 마커      |

---

## 배운 점

1. **LLM 최적화 및 파인튜닝**
   - LLM을 일반 컴퓨터에서 실행하려면 **양자화(Quantization)**가 중요하다.
   - LLM 파인튜닝 시, 특정 상황을 잘 구분할 수 있는 다양한 질문-대답 세트를 만들어야 한다.

2. **STT 모델 한계**
   - 한국어 STT 모델이 크기가 크고, 로컬 환경에서는 잘 작동하지 않아 인터넷 연결이 필요하다.
   - 한국어 모델은 양자화 시 성능이 저하되는 경향이 있다.

3. **시스템 통합의 복잡성**
   - 각 기능은 개별적으로 잘 작동했지만, 전체 시스템으로 통합 시 환경 충돌, 실시간 동작 구현, 기존 코드 수정 등이 많은 난관이었다.

4. **로봇 테스트 시 주의사항**
   - 실제 환경에서 코드를 실험하는 것은 매우 위험할 수 있으므로 **로봇 시뮬레이션 환경**이 중요하다.

5. **팀워크 및 코드 통합**
   - 여러 사람이 작성한 코드를 통합하거나 개선된 코드를 재통합할 때 소통과 연결 과정이 어렵다는 점을 배웠다.

---

## 문제 해결

### 픽업존 센서 문제

**상황**: 
- 프로젝트 진행 중 픽업존 센서를 사용할 수 없었습니다. 기존 ARIS 시스템에서는 픽업존 센서가 컵 위치를 자동으로 로봇에 전달했으나, 이 프로젝트에서는 센서를 사용할 수 없었습니다.

**해결 방법**:
- **객체 인식 기술**을 도입하여 컵의 위치를 감지했습니다. 
  - Boundary Box를 설정한 뒤, 컵이 그 안에 3초 동안 머물러 있으면 컵이 놓였다고 인식하고, 프로그램이 컵의 위치를 입력값으로 받도록 구현했습니다.

### 컵과 손 인식 문제

**상황**: 
- 데이터 수집 시 컵과 손이 같이 있는 경우만 학습을 시켜, 손이 없으면 컵을 인식하지 못하는 문제가 발생했습니다.

**해결 방법**:
- 컵만 있는 사진을 추가로 수집해 재학습을 진행했습니다.
- 이를 통해 손이 없어도 컵을 Confidence Level 94% 이상으로 높은 정확도로 인식할 수 있었습니다.

---

## 문제 해결 접근법

1. **문제 해결 습관**
   - 오류를 만났을 때 최소 30분간 스스로 해결하려고 노력했습니다.
   - 이를 통해 문제 이해도가 높아지고, 해결한 경우 다른 사람에게 쉽게 설명할 수 있었으며, 유사 문제 발생 시 스스로 해결할 수 있었습니다.

2. **시뮬레이션의 중요성**
   - 로봇 작업 시 실제 환경에서 테스트하기 전에 시뮬레이션을 통해 경로와 동작을 점검하는 것이 중요했습니다.
   - 잘못된 경로 설정은 로봇 충돌 등의 위험을 초래할 수 있습니다.

3. **개발자 노트**
   - 오류, 명령어, 해결 방법 등을 체계적으로 기록하여 문제 해결 속도를 크게 향상시켰습니다.
   - 팀원들과 노트를 공유하면 협업의 효율이 배가되었습니다.



