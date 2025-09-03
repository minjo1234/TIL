
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



1.choose a mountpoint mountpoint 

```bash
sudo mkdir -p /mnt/data

```


2.vi etc/fstab 




### MountPoint 

- it is a location that filesystems connect to directory
- to use in linux disk(ex) partition) -> make a filesystem and format -> must have to mount in directory
- Mount point is a connect point a "what about directory connect to directory"


RealtionShip

[Physical Disk] --> [LVM: VG → LV] --> [Filesystem] --> [Mount Point (/data, /mnt/data, ...)]

- LVM = 저장 공간을 논리적으로 쪼갬
- Filesystem = 데이터를 관리할 구조(ext4, xfs 등)
- Mount Point = LV+FS를 실제 디렉토리에 연결

---

```
lsblk -f
```

```
sda4      LVM2_m LVM2 ...

└─ubuntu--vg-data   ext4  UUID=7ddeb29d-be96-47b1-8e63-4f6a9525ea80
```

```
### **3. Create a mount point**

sudo mkdir -p /mnt/data
```

```
### **4. Mount manually (test)**

sudo mount /dev/ubuntu--vg/data /mnt/data
```


```
root@vm-uw4m:/mnt/data# sudo mount /dev/mapper/ubuntu--vg-data 
```


- /dev/mapper/ubuntu--vg-data
    
    → 이건 **장치 파일(디바이스 노드)** 이름. **무엇을 어디에 붙일지**에서 “무엇(=장치)”에 해당.
    
    → 1.LVM은 보통 /dev/mapper/VG-LV 경로를 제공합니다. 
- 어떤 배포판은 /dev/VG/LV(예: /dev/ubuntu--vg/data) **심볼릭 링크**도 같이 만들어주는데, 환경마다 없을 수 있어요. 
- 2.그래서 이전에 /dev/ubuntu--vg/data로는 “없음” 오류가 났던 겁니다.



```bash

# specific directories mount check
findmnt /mnt/data
df -h | grep /mnt/data
```


/etc/fstab


---

### Linux FileSystem (/etc/fstab)

/etc/fstab 

- when the use change partition information and append disk, the user must have to register this file 
- composed 6 fields - 

```
[파일_시스템_장치]  [마운트_포인트]  [파일_시스템_종류] [옵션] [덤프] [파일체크_옵션]

출처: [https://meongj-devlog.tistory.com/134#google_vignette](https://meongj-devlog.tistory.com/134#google_vignette) [기록하는 습관.:티스토리]
```

---


Links : 



Linux FileSystem : https://meongj-devlog.tistory.com/134#google_vignette
