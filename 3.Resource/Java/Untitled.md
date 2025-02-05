

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