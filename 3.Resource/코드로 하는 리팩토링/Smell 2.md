
##  1.Duplicated Code

- Disadvantage  
1. you look carefully, is it similar or the same?
2. when you change code, chagne the code of all of same that

- Usable of Refactoring Structure
	1.Extract Function - use the same code on the several method
	2.Slide Statements If you look at the code, similar but does not same 
	3.Pull Up Method - Several Subclass on the same code 

---

## Extract Function (Option, Command + M )

Seperate Into Intent and Implementation 

Intent : Simple Function and understand easily 
Implementation : You lead the code that try to find out meaning of the code, there is Implementation

1.Write Information of the Function 

and read the code, but you try to find out meaning of the code 
you think it Implementation, 

2.and use Extract Method 

Seperate it accroding to its function 
Connect, Read, Print 

---

# Slide Statements (Shift, Option + L)

- You can understand easily, when the related code tied up  


---

# Pull Up Method

- Duplicated code can be used well, but future provides an excuse of the causing bug 
-  the same code of the several subclass, you can apply easily 
-  similar code but portion value different, "ParameterLizing Function", you can apply after refactoring 
- if subclass depend on parent class, can be applied after applying the field "raising method"
- Two methods follow. similar procedure, you consider "template method fattern" 

---

