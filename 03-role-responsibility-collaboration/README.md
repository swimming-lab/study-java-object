# 3장. 역할, 책임, 협력

객체지향 패러다임의 관점에서 핵심은 역할(role), 책임(responsibility), 협력(collaboration)이다.

객체지향의 본질은 협력하는 객체들의 공동체를 창조하는 것이다.

**협력**

객체를 설계하는데 필요한 일종의 문맥이다.

객체지향 시스템은 자율적인 객체들의 공동체이다.

두 객체 사이의 협력은 하나의 객체가 다른 객체에게 도움을 요청할 때 시작된다.(메시지 전송)

객체는 다른 객체의 상세한 내부 구현에 직접 접근할 수 없기 때문에 오직 메시지 전송을 통해서 커뮤니테이션을 한다.

**책임**

할 일은 협력에 필요한 행동을 수행할 수 있는 적절한 객체를 찾는 것이다. 이 때 협력에 참여하기 위해 객체가 수행하는 행동을 책임라고 한다.

객체에 의해 정의되는 응집도 있는 행위의 집합으로, 객체가 유지해야 하는 정보와 수행할 수 있는 행동에 대해 개략적으로 서술한 문장이다.

객체가 ‘무엇을 알고 있는가', ‘무엇을 할 수 있는가'로 구성된다.

- 하는것 (Doing)
    - 객체를 생성하거나 계산을 수행하는 등의 스스로 하는 것
    - 다른 객체의 행동을 시작시키는 것
    - 다른 객체의 활동을 제어하고 조절하는 것
- 아는 것(Knowing)
    - 사적인 정보에 관해 아는 것
    - 관련된 객체에 관해 아는 것
    - 자신이 유도하거나 계산할 수 있는 것에 관해 아는 것

영화 예매 시스템을 구성하는 역할과 책임(CRC카드)

[캡처]

중요한 것은 객체의 상태가 아니라 행동이다. 객체가 가질 수 있는 상태는 행동을 경하고 나서야 비로소 결정할 수 있다.

협력이 객체의 행동을 결정하고 행동이 상태를 결정한다. 그리고 그 행동이 바로 객체의 책임이 된다.

**Infomation Export 패턴**

자율적인 객체를 만드는 가장 기본적인 방법은 책임을 수행하는 데 필요한 정보를 가장 잘 알고 있는 전문가에게 그 책임을 할당하는 것이다.

**책임 주도 설계(Responsibility-Dreven Design, RDD)**

어떤 책임을 선택하느냐가 전체적인 설계의 방향과 흐름을 결정한다. 이처럼 책임을 찾고 책임을 수행할 적절한 객체를 찾아 책임을 할당하는 방식으로 협력을 설계하는 방법을 책임 주도 설계라 한다.

협력은 객체를 설계하기 위한 구체적인 문맥을 제공한다. 협력이 책임을 이끌어내고 책임이 협력에 참여할 객체를 결정한다. 책임 주도 설계는 자연스럽게 객체의 구현이 아닌 책임에 집중할 수 있게 한다.

과정

- 시스템이 사용자에게 제공해야 하는 기능인 시스템 책임을 파악한다.
- 시스템 책임을 더 작은 책임으로 분할한다.
- 분할된 책임을 수행할 수 있는 적절한 객체 또는 역할을 찾아 책임을 할당한다.
- 객체가 책임을 수행하는 도중 다른 객체의 도움이 필요한 경우 이를 책임질 ㄱ적절한 객체 또는 역할을 찾는다.
- 해당 객체 또는 역할에게 책임을 할당함으로써 두 객체가 협력하게 한다.

**역할**

객체는 협력이라는 주어진 문맥 안에서 특정한 목적을 갖게 된다. 객체의 목적은 협력 안에서 객체가 맡게 되는 책임의 집합으로 표시된다.

객체가 어떤 특정한 협력 안에서 수행하는 책임의 집합을 역할이라고 한다.

역할은 다른 것으로 교체할 수 있는 책임의 집합이다.

교재에서는 AmountDiscountPolicy, PercentDiscountPolicy 두 종류의 구체적인 객체를 포괄하는 DiscountPolicy 인터페이스(추상화)가 역할이다.(역할을 구현하는 가장 일반적인 방법: 인터페이스, 추상클래스)

요점은 동일한 책임을 수행하는 역할을 기반으로 두 개의 협력을 하나로 통합할 수 있다는 것이다.

동일한 책임을 서로 다른 방식으로 수행할 수 있는 객체들이 필요해질 때 역할을 도입하면 된다.