---
layout: post
title: Performance Testing 정리 3
tags: [Test, Ipsum, Markdown, Portfolio]
---

# Performance Testing 3 

### Chapter3. 성능 테스트시 어떤 위험사항이 있을까

속도, 확장성, 안정성 세가지의 카테고리로 해결할 수 있는 위험을 고려하는 것이 중요하다.

- Capacity
  - 정상 또는 최대 부하 상태일때 시스템 용량이 비즈니스 볼륨을 충족하는가?
- Compennet
  - 구성요소는 기대치를 충족하는가? 
  - 합리적으로 최적화가 잘 되있는가? 
  - 구성요소로 인한 성능 이슈가 관찰되는가?
- Endurance
  - 성능이 시간이 지나도 동일하게 유지가 되는가?
  - 성능을 느리게 성장하는 문제를 아직 발견하지 못했는가?
- Investigation
  - 시간에 따른 성능 트렌드를 파악하는 방법은 어떤건가요?
- Load
  - DB,파일 서버에서 다룰 수 있는 데이터 양은 얼마나 많나요?
  - 네트워크 구성요소는 적절한가요?
- Smoke
  - 추가적인 성능 테스트를 위해 빌드가 준비되어 있나요? 다음에는 어떤 성능 테스트를 수행하나요?
- Spike
  - 만약 예상했던 최대 부하를 초과하면 생산 부하는 어떤일이 발생하나요?
- Stress
  - 만약 예상했던 부하를 초과하면 생산 부하는 어떤일이 발생하나요?
- Unit
  - 코드의  세그먼트가 합리적으로 효율적인가?
- Validation
  - 어플리케이션이 요구사항과 목표를 충족하는가?
  - 이 버전이 이전 버전보다 빠르거나 느린가?

#### 속도 관련 위험

속도 관련 위험은 유저가 먼저 생각하는 것 일지라도 유저 만족도에 국한되지 않는다. 속도는 비즈니스, 데이타 관련 위험 요소이기도 하다.  속도 문제를 성능 테스트로 해결 할 수 있는것들은 다음과 같다. 

- 어플리케이션이 유저를 만족시킬만큼 빠른가?
- 어플리케이션이 최신 정보를 제공할 수 있는가?
- 에러가 나기 전에 예상된 최대 응답 시간시간 내에 응답하는가?

이를 해결 또는 완화하기 위한 방법으로는 다음과 같다.

- 경쟁 제품 또는 버전과 속도를 비교해봐라
- 정상 또는 최대 부하일때의 워크로드를 복제하여 부하 테스트를 설계해봐라 ( 사용량이 급증할때의 상황을 비슷하게 만들고 테스트 )
- 성능 테스트 결과를 투자자들에게 도움을 요청해라
- 예상된 최대 부하 상태에서 사용자들에게 피드백을 얻어봐라
- 성능 테스트에 시간이 중요한 트랜잭션을 포함하라
- 다양한 조건에서 부하 수준, 시나리오를 혼합해서 속도 측정을 해봐라 ( 사용자는 변함없는 속도에 중요하게 생각함 )

#### 확장성 관련 위험

어플리케이션이 지원할 수 있는 유저의 수 뿐만 아니라 어플리케이션이 포함하고 처리할 수 있는 데이터의 양, 용량에 도달하기 까지의 시기를 확인할 수 있는 기능과 관련이 있다.

- 전체 유저를 위한 받아들일 수 있는 응답 시간과 일관되게 제공을 할 수 있는가?
- 어플리케이션의 생명 주기 동안 수집된 데이터를 저장할 수 있는가?
- 최대 용량에 다 다랐을때 경고를 알려주는가?
- 헤비 사용량에 어플리케이션이 여전히 안전한가?
- 헤비 사용량에 기능이 손실되는가?
- 예상치 못한 최대 부하를 견딜 수 있는가?

완화 하는 전략으로는 다음과 같다.

- 다양한 부하에서 측정된 속도를 비교하라
- 예상된 최대 시간과 일반적인 상황에서 워크로드를 복제하여 부하 테스트를 설계하라
- 실제 요구사항에 매핑되는 의미있는 성능 테스트를 한다.
- 실제 생산중에 수행되는 비즈니스 운영과 비슷한 용량, 타입, 유통으로 성능 테스트를 실시하라.

#### 안정성 관련 위험

안정성은 회복 능력, 가동 시간, 신뢰성과 같은 전반적인 용어이다. 안정성 위험은 안정성 이슈, 내구성, 고부하 ,스트레스 테스트와 함께 일반적으로 해결되는데 가장 기본적인 성능 테스트에서 안정성 이슈가 때때로 감지된다.

- 데이터 손상, 속도 저하 없이 오래 시간동안 어플리케이션이 구동되는가?
- 만약 예기치않은 오류로 다운되면 부분적으로 완료된 트랜잭션은 어떻게 되는가?
- 시스템을 다운시키지 않고 업데이트를 할 수 있는가?
- 반복적인 기능적 오류의 조합으로 시스템 충돌이 일어날 수 있는가?
- 예기치 않게 시스템이 중단된 경우 다시 정상적으로 작동을 할 때  올바른 시점에 작동할 수 있는가?

완화 전략으로는 다음과 같다.

- 현실적인 내구성 테스트를 위한 시간을 만들어라
- 주요 시나리오로 스트레스 테스팅을 실시해라 ( 비즈니스 지표 참고 )
- 오프라인 테스트를 실시하여 데이터 무결성, 성능, 기능을 관찰하라
- 성능 테스트 중에 패치를 적용한다.
- 성능 테스트중에 바이러스/백업을 강제로 실시해봐라
- 성능 테스트 시나리오에 오류와 예외상황을 추가하라.