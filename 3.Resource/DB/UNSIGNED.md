
- 기본적으로 UNSIGNED 타입을 지정하게 되면 -2,147,483,648에서 2,147,483,647까지의 값을 저장할 수 있는 범위가 0에서 4,294,967,295까지 확장됩니다.

```SQL
CREATE TABLE example (
id INT UNSIGNED NOT NULL AUTO_INCREMENT, 
value INT UNSIGNED, PRIMARY KEY (id) 
);

```

