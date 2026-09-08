
- Mother Board : 
	- MSI PRO B660M-A WIFI DDR4
	- Lay out Guide : https://www.youtube.com/watch?v=7NeYAi5go2g
- **Processor** :
	- 12th Gen Intel(R) Core(TM) i5-12400F
- **Ram Corsair Vengence LPX : 16GB + 16GB** :
	- CMK16GX4M1Z3600C18
	- CMK16GX4M1E3200C16
- **SSD: 512GB + 1TB** :
	- XPG GAMMIX S5 : 512GB
	- PNY CS1030 1TB SSD : 1TB




#### Commands:

Mother Board:
```
wmic baseboard get manufacturer,product,version,serialnumber
```

Processor:
```
wmic cpu get name,numberofcores,maxclockspeed
``` 

Ram:
```
wmic memorychip get manufacturer,partnumber,formfactor
```

SSD:
```
wmic diskdrive get model,size,interfacetype
```


