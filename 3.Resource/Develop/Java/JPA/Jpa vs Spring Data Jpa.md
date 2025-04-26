
public class MemberRepository {  
  
    @PersistenceContext  
    private EntityManager em;  
  
}

public interface MemberRepository extends JpaRepositories<> 


jpql 만들어서 넣어두기.


SELECT parent.id AS parent_id,  
       parent.name AS parent_name,  
#        st.id AS child_id,  
#        st.name AS child_name,  
#        st.productTypeId AS child_productTypeId,  
       st.solutionType,  
  
#        s.id AS sale_id,  
       sum(s.totalCost)  
  
FROM solution parent  
         LEFT JOIN solution  
             st ON parent.id = st.productTypeId  
         LEFT JOIN sale s ON s.solutionId = st.id  
WHERE parent.productTypeId IS NULL  
#   and st.solutionType = 'SOFTWARE'  -- 이 자리에는 변수가 올것같음  
  AND s.solutionId = st.id  
group by parent.id;  
  
select * from solution;  
select * from sale;
