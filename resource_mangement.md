# Resource Management in OED
Open Ethernet Drive uses embedded Debian OS on its proprietary hardware, so the resource management is a little different than 

## RM in general
- Control groups (CG) 
	- CG can manage linux subsystem such as CPU, memory, disk, network, etc.
	- Have 2 versions: 1) use ```libcgroup``` 2) via ```systemd```
	- Neither have working solution for OED.
- ```ulimit```
	- Used for RAM control
	- We can use ulimit -v [size] to modify the virtual memory size for a process. Once set, the RAM limit is hard limit and cannot increase but only decrease. Logout then login again will reset the limit. 
	``` 
    $ ulimit -v
	unlimited
	$ python -c '[ "x" * 100000000 ]'
	$ ulimit -v 100000
	$ python -c '[ "x" * 100000000 ]'
	Traceback (most recent call last):
	  File "<string>", line 1, in <module>
	MemoryError
	```
    
- ```cpulimit```
- ```quota``` for disk I/O related management
