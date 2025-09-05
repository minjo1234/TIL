### Fact Table vs Dimension (Star Schema)

확인이유 : 자원수집 관련한 테이블중 
- dimension 
- fact 
- real table(vm)
- data warehouse - need to search 
- star schema - https://sunrise-min.tistory.com/entry/Star-schema%EC%99%80-Snowflake-schema-%EB%B9%84%EA%B5%90
- data warehouse(DW) - https://bomwo.cc/posts/Datawarehouse/


     
```text
vm (Master Table)
↓ (1:1) 
dimension_sddc_vm (Dimension Table)  
↓ (1:1) 
fact_sddc_vm_dimensions (Fact Table - Bridge)
    ↓ (1:Many) 
fact_vm_metric (Metrics Data) 
fact_vm_metric_day (Daily Aggregated Metrics)
fact_vm_billing_day (Daily Billing Data)
```

- why this structure prefer ? 

vm.id -> fact_vm_metric.vmId 
vm.id -> dimension_sddc_vm.vmId -> fact_sddc_vm_dimensions_vmId  


### 1. 새로운 자원 수집 시 - Fact 테이블만 추가

```
-- 기존 구조 그대로 유지하면서:
-- 새로운 자원 타입 추가
-- 예: GPU 메트릭 수집 시작

CREATE TABLE fact_vm_gpu_metric (

id BIGINT PRIMARY KEY,
dimensionId BIGINT, -- 기존 fact_sddc_vm_dimensions.id 사용
gpuUsage DOUBLE,
gpuMemoryUsage DOUBLE,
createdTime DATETIME
);

-- 기존 dimension 테이블들은 전혀 변경 불필요!
-- fact_sddc_vm_dimensions.dimensionId만 참조하면 됨

```


###  Master 테이블 변경 시 - Dimension만 수정

```
-- 1. Master 테이블 변경

ALTER TABLE vm ADD COLUMN securityLevel VARCHAR(20);

-- 2. Dimension 테이블만 수정

ALTER TABLE dimension_sddc_vm ADD COLUMN securityLevel VARCHAR(20);

-- 3. Fact 테이블들은 전혀 영향받지 않음!
-- fact_vm_metric, fact_vm_billing_day 등은 그대로 유지
```

### 인덱스로 조회 효율성 dimension_Id 


- 상황부여 : 원래는 vCenter에서 제공하는 30일의 자원만 수집하려고 하였는데 
  일자별로 평균값을 원하였다. 그 상황에서 GPU VM이라는 특수한 case의 자원수집을 원하다보니 원본테이블의 변경을 할 지 고민하던중 start schema 를 적용하기로 하였다. - dimension, fact  - 이 상황을 해결하고자 startSchema를 고안해냈으며 수정완료했다.
- 
