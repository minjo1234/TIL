### findById() vs getReferenceById()


| 조건      | findById        | getReferenceById   |
| ------- | --------------- | ------------------ |
| 레파지토리  | CrudRepository  | JpaRepository      |
| 값이 없을경우 | Optionl.empty() | 오류발생               |
| 성능      |                 | 참조값만 가져온 후 데이터가 필요 |
|         |                 |                    |
