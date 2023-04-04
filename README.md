# 자동 재고 확보 시스템을 위한 MSA

## 시나리오
<도넛-스테이츠>는 온라인으로 도너츠를 판매합니다.
웹사이트를 통해서 주문 버튼을 누르는 것으로 구매(Sales API)가 가능합니다.
창고에 재고가 있다면 재고가 감소하고 구매가 완료됩니다.
유튜브스타 김깜빡 님이 도넛-스테이츠의 도너츠가 맛있다고 영상을 올렸습니다.
그를 따르는 데브옵스 수강생들이 몰려듭니다. 주문이 급등합니다.
창고에 재고가 없기 때문에 구매가 불가능한 경우가 발생합니다.
창고의 도너츠 재고가 다 떨어지면 제조 공장에 알려서 다시 창고를 채우는 시스템을 구축해야합니다.
제조 공장인 <팩토리-스테이츠>에 주문을 요청(Leagcy Factory API)할 수 있습니다.
주문이 요청되면 일정 시간이 지난 후 창고에 재고가 증가합니다.

<br/>

## 구성요소
1. Sales API
2. Factory API
3. 프론트엔드(웹사이트) : cURL / postman / k6 등을 통한 API 호출로만 구현
Sales API를 통해 백엔드에 요청
4. 백엔드(서버) : 구매 시 창고에서 재고 확인 후 재고 감소 로직 구현
재고가 부족할 경우 Factory API를 통해 재고 확보 요청
데이터베이스(창고) : RDS에 mysql db 구성
요청에 따른 재고 상태 변경

<br/>

## 요구사항
<details>
<summary>요구사항 1</summary>

<!-- summary 아래 한칸 공백 두어야함 -->
1. Sales API 를 통해 요청을 받은 서버가 데이터베이스에서 재고 상황을 확인합니다.
2. 재고가 있다면 감소시키고 응답으로 판매완료 내용을 전달합니다.
3. 재고가 없는 경우 공장에 주문을 진행합니다
4. 재고가 없다는 내용을 담은 메세지 페이로드가 주제별로 생성됩니다.
5. 메세지가 느슨하게 연결된 시스템을 통해 처리될 수 있도록 따로 보관됩니다.
</details>
<details>
<summary>요구사항 2</summary>

<!-- summary 아래 한칸 공백 두어야함 -->
1. 빈번한 요청으로 메세지 누락이 발생합니다.
2. 메세지가 처리되지 않은 경우 메세지들을 체계적으로 관리할 다른 처리 공간을 생성해야합니다.
3. 메시지 처리 보관 리소스와 처리되지 않은 메세지 처리 리소스가 연결되어야합니다.
</details>
<details>
<summary>요구사항 3</summary>

<!-- summary 아래 한칸 공백 두어야함 -->
1. 안정적으로 이벤트가 전달 될 수 있는 시스템을 구축해야합니다.
2. 메세지를 소비하는 리소스를 통해 Factory API가 호출됩니다.
3. 수신된 메세지에 의해 트리거가 된 컴퓨팅 리소스가 상품 재고를 증가시킵니다.
</details>


## Step 1: Serverless를 이용한 Lambda 생성

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step1.png)


## Step 2: Serverless를 이용한 Lambda - SQS - Lambda 구조 생성

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step2.png)

## Step 3: DLQ 연결 및 K6 성능테스트

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step3.png)
