
Only one instance of the class 

```
public static Settings getInstance() {  
    if (instance == null) {  
        instance = new Settings();  
    }  
  
    return instance;  
}
```

this code has multi thread enviorment not saft

### so we can use double checked locking 

----

### 1.using volatile

`private static volatile Settings instance;`

---

### 2.static inner 

```
private static  class  SettingsHolder {  
    private static final Settings  INSTANCE = new Settings();  
}  

public static Settings getInstance() {  
    return SettingsHolder.settings;
    
```
`

###  3.Serialize (ObjectOutputStream, ObjectInputStream)


```
Settings settings = Settings.getInstance();  
Settings settings1 = null;  
  
try (ObjectOutput out = new ObjectOutputStream(new FileOutputStream("settings.obj"))) {  
    out.writeObject(settings);  
}  
  
try (ObjectInput in = new ObjectInputStream(new FileInputStream("settings.obj"))){  
    settings1 = (Settings) in.readObject();  
}

```

enum do not allow reflectively 
but enum has disadvantage, already make the class of the build app 

---

recommend 2 methods

### 1.static inner 
### 2.use enum type

```
public enum Settings {  
    INSTANCE;  
}
```



- method of the implement singleton Pattern  do not use enum Type  

1.static Inner (ex Holder)

- disadvantage of method using private constructor and static method 

1.reflectively not safe

- if you make singleton patter by using enum type, advantage and disadvantage that ?

1.advantage : enum type is safe reflectively
2.disadvantage : when build app, enum type class already making 
	3.disadvantage : can't use inheritance X

- Let's implement singleton pattern using static inner class 


---

When you use static Inner class, If you make a newInstance() 
you can use this method 


### 1.reflection 

```
Constructor<Settings> constructor = Settings.class.getDeclaredConstructor();  
constructor.setAccessible(true);  
Settings settings2 = constructor.newInstance(settings);

```

### 2.Serialize 

```
try (ObjectOutput out = new ObjectOutputStream(new FileOutputStream("settings.obj"))){  
    out.writeObject(settings);  
}  
  
try (ObjectInput in = new ObjectInputStream(new FileInputStream("settings.obj"))) {  
    settings1 = (Settings) in.readObject();  
}
```


---

### On Site

1.Singleton scope, one of the bean scopes in Spring 
2.java java.lang.Runtime
3.Other Design pattern(builder, fasade, abstract factory) used by partition of embodiment 

-----

you can use On Spring

```
ApplicationContext applicationContext = new AnnotationConfigApplication(SpringConfig.class)

String hello = applicationContext.getBean("hello, String.class);

String hello2.= applicationContext.getBean("hello", String.class);
System.out.println(hello == hello);


```


this is not a singleton pattern, but spring maintains the object in springObject 


