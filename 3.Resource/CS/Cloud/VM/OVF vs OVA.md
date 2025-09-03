
## OVF file and OVA Component  - Blog 

### OVF vs OVA 

OVF - A directory of files - Large VMs , Download available , four files 
OVA - A single tar - Easier to distribute, 


Disk Usage - same 


### Make a ova 

```
tar -cvf vmName.ova  vmName.ovf  vmName.mf  vmName-disk1.vmdk
```

.ovf (descriptor) - xmlFile, Metadata 
.mf (manifest) - all of the package file, not essential 
.cert - authentication with mf file, not essential 
.vmdk (disk, tihin-provisioned) - for distribution and compress 
CD seperate