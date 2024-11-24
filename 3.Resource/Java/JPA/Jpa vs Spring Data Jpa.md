
public class MemberRepository {  
  
    @PersistenceContext  
    private EntityManager em;  
  
}

public interface MemberRepository extends JpaRepositories<> 

		
