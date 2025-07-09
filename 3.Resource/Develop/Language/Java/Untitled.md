

case when :#{#condition.orderColumn} = 'issuanceDate' THEN MAX(si.issuanceDate) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'projectName' THEN MAX(bd.projectName) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'salePayment' THEN MAX(si.salePayment) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'salesManager.name' THEN MAX(u.name) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'revenueCompany.name' THEN MAX(c.name) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'saleCostSum' THEN MAX(bd.saleCostSum) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'cost' THEN SUM(si.cost) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'notComplete' THEN MAX(bd.projectName) else null end :#{#condition.direction},  
case when :#{#condition.orderColumn} = 'revenueType' THEN MAX(bd.revenueType) else null end :#{#condition.direction}



and (:#{#condition.salesManagerId} is null or bd.salesManagerId = :#{#condition.salesManagerId})

departmentId는 매년변경된다.


mysqldump --triggers --routines -u erp -p erp > mysqldump2.sql

productTypeId IN (1, 2, 4, 42, 11, 196)

![[Pasted image 20250206110241.png]]

![[Pasted image 20250206111549.png]]


![[Pasted image 20250206111558.png]]
윤귀형
박창식
백두홍
이진호

최윤석 - x 


|   |
|---|
|윤귀형|

|     |
| --- |
| 이양우 |



엑셀 기준으로 반영하였습니다.
엑셀에는 존재하지 않는 분이 한 분 계시는데 (영업 1본부 이진호 부장)
육아휴직 중이라고 하셔서 영업 목표에는 반영해 두었습니다.
수정 필요하면 말씀부탁드리겠습니다!