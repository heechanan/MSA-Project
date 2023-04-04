# 자동 재고 확보 시스템을 위한 MSA

## 시나리오
<도넛-스테이츠>는 온라인으로 도너츠를 판매합니다.
웹사이트를 통해서 주문 버튼을 누르는 것으로 구매(Sales API)가 가능합니다.
창고에 재고가 있다면 재고가 감소하고 구매가 완료됩니다.
유튜브스타 hoyong.LEE가 도넛-스테이츠의 도너츠가 맛있다고 영상을 올렸습니다.
그를 따르는 데브옵스 수강생들이 몰려듭니다. 주문이 급등합니다.
창고에 재고가 없기 때문에 구매가 불가능한 경우가 발생합니다.
창고의 도너츠 재고가 다 떨어지면 제조 공장에 알려서 다시 창고를 채우는 시스템을 구축해야합니다.
제조 공장인 <팩토리-스테이츠>에 주문을 요청(Leagcy Factory API)할 수 있습니다.
주문이 요청되면 일정 시간이 지난 후 창고에 재고가 증가합니다.



## Step 1: Serverless를 이용한 Lambda 생성

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step1.png)


## Step 2: Serverless를 이용한 Lambda - SQS - Lambda 구조 생성

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step2.png)

## Step 3: DLQ 연결 및 K6 성능테스트

![](https://contents-img-jeonghun.s3.ap-northeast-2.amazonaws.com/project3/project3-tutorial-step3.png)
