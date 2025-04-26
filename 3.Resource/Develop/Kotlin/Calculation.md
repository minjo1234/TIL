
### identity = === 
### equality = == , eqauls 


if you use Overiding method eqauls, hashcode 

```
@Override  
public boolean equals(Object o) {  
    if (this == o) return true;  
    if (o == null || getClass() != o.getClass()) return false;  
    JavaMoney javaMoney = (JavaMoney) o;  
    return amount == javaMoney.amount;  
}  
  
@Override  
public int hashCode() {  
    return Objects.hash(amount);  
}

```


---

- in / !in
- a..b
- a[i]
- a[i] = b
