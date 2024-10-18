
If the situation of HelloController uses SimpleHelloSerive 
HelloController has dependence by SimpleHelloSerive

If the situation of SimpleHelloService changes,
the dependent class must change its code 

---
2.
HelloController -> <<interface>> HelloService 
			SimpleHelloSerive ,  ComplexHelloService


In this relationship, you might think that the class is generally 
free to use, but this is not the case 

But HelloController Since we do not know which class the HelloService interface refers to, we need to create a relationship, which is called DI

this called Assembler 
It takes classes that originally has no direct dependencies,
connects them, and makes them usable,

Assembler = Spring Container

You can use a three method 

1.make constructor 
2.factory method 
3.using setter 

------------------------------------------------------------------------

Mapping is a how controller method executes request


