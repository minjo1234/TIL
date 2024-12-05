### findById() vs getReferenceById()


| 조건      | findById        | getReferenceById                  |
| ------- | --------------- | --------------------------------- |
| 레파지토리  | CrudRepository  | JpaRepository                     |
| 값이 없을경우 | Optionl.empty() | 오류발생                              |
| 성능      | 전체조회            | 참조값만 가져온 후 데이터가 필요해질경우 지연로딩 = 더좋음 |
|         |                 |                                   |

### 즉시로딩 vs 지연로딩

즉시로딩 : **엔티티를 조회할 때 연관관계에 있는 엔티티도 함께 조회하는 방법**
