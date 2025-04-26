
### nullable 

---
### toMethod 

- toLong 
- toDouble 

---
### Object Type - Smart Cast 

```
fun printAgeIfPerson(obj: Any){  
    if (obj is Person) {  
        val person = obj as Person  
        println(person)  
    }}


instnaceof = is
(Person). -> obj as Person 
obj.age ok 

```

```
  
fun printAgeIfPerson(obj: Any?){  
    val person = obj as? Person  
    println(person?.age)  
}
```

----

### Kotlin specific Type 

### 1.Any

- Object role of Java ( Top Type of all of the object )
- Every primitive type top type is Any 
- Any do not express nullable so you can use Any?
- Any has equals, hashcode, toString  

---

### 2.Unit

- Unit is a Java  Void
- Unit use the type ifself  different from void 
- In Functional Programming Unit means singleton instance of the type , Unit is a actually exist type,  
---

### 3.Nothing

- Nothing means function doesn't end normally
- Unconditionally return exception 
---


### String interpolation / String indexing 

#### Tip 

use ${variable}
trimIndent()

---

Method of deal with Type in Kotlin

- is !is, as, aa?  (is -> judge data type)
- as (cascading)
- Any is top type of java object
- Unit == java void
- Nothing means function doens't end normally 

---

### Method of Kotlin Type

- use ${variable}} and """""""" can make neat coading

