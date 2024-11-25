
public class MemberRepository {  
  
    @PersistenceContext  
    private EntityManager em;  
  
}

public interface MemberRepository extends JpaRepositories<> 


jpql 만들어서 넣어두기.
