
**LVM(Logical Volume Manager) Concept and Setting Rule** 

LVM is a part of kernel that management space efficiently and flexible 

in case that does not LVM, operation after mount Disk on the OS region 

기존은 하드디스크를 파티셔닝 한 후 OS 영역에 마운트 하여 read/write를 수행하기 때문에 수정이 어렵다. 
LVM은 파티션 대신에 volume이라는 단위로 저장 장치를 다룬다.
expand, change flexible for storage, they don't have to move 
when they resizing 



```
```


lsblk -f
