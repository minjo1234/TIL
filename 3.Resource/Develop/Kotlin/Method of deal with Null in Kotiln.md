
you can use ? 

```
fun startWithA2(str : String?): Boolean ?{  
    if(str == null) {  
        return null;  
    }  
    return str.startsWith("A")  
}
```

---

### safe call

```
    val str: String? = "ABC";  
    println(str?.length)  
    str?.length ?: 0
```

---

###  nullable, but surely not null 

```
fun startWith4(str : String?): Boolean {  
    return str!!.startsWith("A")  
}
```

---

### Java And Kotiln

```

-- getName() 
@Nullable  
public String getName() {  
    return name;  
}


-- kotiln -- 
fun stratWithA(str: String?): Boolean {  
    return str?.startsWith("A") ?:false;  
}

```


---

- Kotlin thinks about 
- Safe call 
- Elvis 연산자 (? : )
-  !! 
- platform type
- Java -> Kotiln