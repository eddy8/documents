# 루프 링이란 무엇입니까?


루프 링은 분산 토큰 교환 프로토콜입니다. 이것은 반복적 인 분산 형 교환 시스템의 핵심 인 에레 멘텀 스마트 계약으로 구현됩니다. 이 디자인은 전통적인 중앙 집중식 교환보다 몇 가지 개선 사항을 허용합니다.

* **거래 상대방 및 Exchange 위험 감소**: 제 3 자 교환기 및 토큰에 디지털 자산을 보관하고 보관하는 위험을 제거하는 것은 주문에 의해 잠기지 않습니다.
* **높은 유동성**: 모든 거래 쌍에서 유동성을 높일 수 있도록 주문이 일치합니다.
* **공정성**: 수수료 및 할인 모델은 관련된 모든 당사자 (제조사, 수취인 및 광부) 간의 공정성을 허용합니다.
* **약한 감독**: 전체 시스템이 완전히 분산되어 있습니다.


[백서](https://github.com/Loopring/whitepaper/raw/master/en_whitepaper.pdf) 에서는 루프 링 프로토콜의 배경과 일반적인 디자인에 대해 자세히 배울 수 있습니다 . 구현을 진행하면서 백서의 일부 세부 사항이 구식이 될 수 있음을 명심하십시오. 차이점이있을 때마다이 웹 사이트를 최신 공식 업데이트로 참조하십시오.



## 왜 ?

루프 링 프로토콜은 중앙 집중식 교환기에서 발견되는 여러 가지 문제를 해결하기 위해 고안되었으며이 페이지 의 [마지막 섹션](overview.md#issues-with-centralized-exchanges) 에 대한 간략한 설명 이 나와 있습니다.



# 생태계

이 섹션에서는 루프 링 생태계의 핵심 부분과 상호 작용 방법을 소개합니다. 그들은 공동으로 제공하는 모든 기능을 공동으로 제공합니다. 각각에 대한 자세한 설명은 아래 링크를 참조하십시오.

**지갑**
> 토큰에 대한 액세스를 제공하고 루프 링 네트워크에 주문을 보내는 방법을 제공하는 일반적인 지갑 서비스 / 인터페이스.

**릴레이**
> 공공 주문서 및 거래 내역을 관리합니다. 다른 릴레이 및 링 광부에게 새로운 주문을 전달합니다. 링 - 마이닝은 릴레이의 한 특징입니다. 그것은 계산 무거운이며 completly off-chain 이루어집니다. 이 프로세스는 최소 2 개의 토큰이 포함 된 일련의 거래를 생성하며 이를 주문 고리라고 합니다.



**루프 프로토콜 스마트 계약**
>광부로부터받은 링 일치 주문을 확인하고 사용자를 대신하여 토큰을 전달하며 광부에게 인센티브를 부여하고 이벤트를 방출하는 스마트 계약 세트입니다. 릴레이 / 주문 브라우저는 주문서와 거래 내역을 최신 상태로 유지하기 위해 이러한 이벤트를 수신합니다.

**자산 토큰 화 서비스**
> loopring에서 직접 거래 할 수없는 자산 간의 다리. 그들은 신뢰할 수있는 회사 나 조직이 운영하는 중앙 집중식 서비스입니다. 사용자는 자신의 자산 (다른 사슬에서 가져온 판금 또는 토큰)을 예치하고 토큰을 발급받을 수 있습니다. 토큰을 반환함으로써 사용자는 자신의 보증금을 돌려받습니다. LRC는 교차 교환 프로토콜이 아니지만 Asset Tokenization Services를 사용하면 Ethereum ERC20 토큰을 다른 블록 체인 자산뿐만 아니라 물리적 자산으로 교환 할 수 있습니다.

> Asset Tokenization Services는 Loopring 프로젝트의 일부가 아닙니다.


## 개요

이것은 각 단계에 대한 설명과 함께 루프 링 네트워크에서 성공적인 주문의 라이프 사이클입니다. 
![](/img/diagrams/loopring-overview.png)

**0 - 사용자가 거래하기를 원함**
>사용자는 X금액에 TokenA대한 Y금액 을 교환하려고합니다 TokenB. 이 비율에 대한 현재 속도 및 주문서는 계전기 또는 네트워크에 연결된 다른 인터페이스 (예 : 주문서 브라우저)가 제공하는 여러 출처에서 찾을 수 있습니다. 일단 준비가되면 지갑 인터페이스를 사용하여 주문 세부 정보를 입력하고 제출합니다. LRC 금액은 광부에게 수수료로 추가 할 수 있습니다. LRC 수수료가 높은 주문은 광부가 먼저 처리 할 수있는 가능성이 더 큽니다.

**1 - ERC20 인증**
>지갑은 루프 링 스마트 계약 이 사용자가 팔고 자하는 X금액 을 처리하도록 허가합니다 TokenA. 이것은 사용자의 토큰을 잠그지 않습니다. 그는 주문이 네트워크에 의해 처리되는 동안 그들을 자유롭게 움직일 수 있습니다. 송금인 잔액이 (광부 또는 루프 링에 의해) 어느 시점에서 점검되고 자금이 충분하지 않은 경우, 이는 축소 된 것으로 간주됩니다. 축소 된 주문은 취소되는 것과 같지 않습니다. 축소 된 주문은 충분한 금액이 주소로 입금되는 경우 축소 된 주문이 자동으로 원래 크기로 조정되며, 취소는 일방적 수동 조작이며 되돌릴 수 없습니다.


**2 - 주문을 네트워크로 보내기**
>승인이 이루어지면 주문 데이터는 발신자의 개인 키로 서명됩니다. 그런 다음 Wallet은 서명을 따라 주문을 네트워크의 하나 이상의 노드 (중계)로 보냅니다.


**3 - 방송**
>주문 접수에서 릴레이는 공개 주문서를 업데이트하고 주문을 다른 릴레이 및 링 광부에게 방송하여 최대한 빨리 주문 처리를 시작합니다.

**4 - 링 광부 (주문 일치)**
>Ring Miners는 주문을 받고 주문서에 추가합니다. 각자는 주어진 환율로 완전하게 또는 부분적으로 그것을 채우려 고 시도합니다. 링 일치 (ring-matching)가 프로토콜이 어떤 쌍보다 높은 유동성을 제공 할 수있는 주된 이유입니다. 이자율이 고객이 요청한 이자율보다 높으면 할인액이 링의 모든 주문에서 공유되며 마진 분할이라고합니다. 광부는 자신의 수수료로 Margin Split을 청구하거나 LRC를 사용자에게 돌려 주거나 LRC 수수료를 유지할 수 있습니다.


**5 - 검증 및 정산**
>링은 루프링 프로토콜 계약에 의해 수신됩니다. 여러 가지 점검을 통해 광부가 제공 한 데이터를 확인하고 링의 주문률 및 사용자 지갑의 토큰에 따라 링을 완전히 또는 부분적으로 해결할 수 있는지 여부를 결정합니다. 모든 점검이 성공하면 계약서는 토큰을 사용자에게 전송 (5a)하고 광부의 수수료 (5b)를 동시에 지불합니다. 이 작업은 원자 적입니다.

어떤 세부 사항은 주문이 루프링 네트워크에 들어갈 때 무슨 일이 일어나고 있는지 이해하기 쉽지 않은 것으로 보입니다. 프로토콜 (주문 취소, 링 매칭, 주문서 및 거래 내역 동기화 등)에 대한 이해를 높이기 위해 [위에 열거 된](overview.md#ecosystem) 생태계의 주요 부분에 대한 문서를 살펴 보는 것이 좋습니다 .



# 중앙 집중식 교환 문제
루프 링과 같은 시스템의 필요성을 더 잘 이해하려면 먼저 중앙 집중식 교환 모델에서 문제를 지적해야합니다.
토큰을 중앙 교환기로 보낼 때 일어나는 일에 대한 매우 단순화 된보기가 있습니다.

![](/img/diagrams/centralized-model.png)

교환을 사용하고 토큰을 교환하기 위해서는 우선 교환기에 토큰을 예치해야합니다. 귀하의 토큰은 교환 원의 지갑으로 보내지고 차용 증서 인 차용 증서 (차용 증서)를 돌려드립니다. 그런 다음 다른 사용자 IOU와 차용 증서를 교환합니다. 마지막으로 철회를 원할 경우 차용 증서를 교환 원에게 돌려 주며 교환 원은 외부 토큰 주소로 토큰을 돌려 보냅니다.

**보안 부족**
> 이 모델에서는 토큰을 제어 할 수 없습니다. 거래소에서 즉각적인 거래가 가능하지만 많은 위험이 따릅니다. 고정 된 계정, 교환 종료, 해킹, 개발자의 실수 등 여러 가지 시나리오가 있습니다.


**투명성 부족**
> 그들이 지갑의 지갑에있을 때 귀하의 토큰에 어떤 일이 생길 수 있습니다. 정확히 무엇을 알 수있는 방법이 없습니다. 거래소가 파산하여 사용자가 그 사실을 알지 못할 때는 항상 너무 늦었습니다.


**유동성 부족**
> 교환 주문서 풀 및 지원되는 토큰 쌍과 만 거래 할 수 있습니다. 거래량이 충분하지 않아 다른 교환기에서 시도 할 수 있고 거래하고자하는 토큰 쌍이 지원되지 않는 경우 다른 쌍과의 간접 거래를 시도하여 원하는 것을 얻거나 자금을 다른 거래소로 이전 할 수 있습니다 교환. 어느 쪽이든 당신은 요금으로 여러 번 치고 돈이 넉넉하지 않습니다.

중앙 집중식 교류가 직면하는 또 다른 문제가 있습니다. 우리는이 모든 것을 여기서 논의하지 않을 것이고, 웹을 통해 주제에 대해 쓰여진 많은 기사를 읽는 것이 좋습니다.
