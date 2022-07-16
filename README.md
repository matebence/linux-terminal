## Linux Directory structure
- /
	- bin/
		`Essential user command binaries`
	- boot/
		`Static files of the boot loader`
	- dev/
		`Device files`
	- etc/
		`Host specific system configuration`
	- home/
		`User home directories`
	- lib/
		`Essential shared libraries`
	- media/
		`Mount point for removable media`
	- mnt/
		`Mount point for a temp mounted file system`
	- opt/
		`Add-on application software`
	- sbin/
		`System binaries`
	- srv/
		`Data for services provided by this system`
		- www/
		- ftp/
	- tmp/
		`Temp files`
	- usr/
		`Multi user utilities and applications`
	- var/
		`Variable files`
	- root/
		`Home directory for the root user`
	- proc/
		`Virtual file system documenting kernel and process status as text files` 


## Basics commands
	
	man ls
	info bash
	ls --help

	ls
	cd
	pwd
	touch
	echo
	clear
	exit

- [Shell commands explained](https://explainshell.com/)


## Environment vars

	EDITOR
	HOME
	LONGNAME
	MAIL
	OLDPWD
	PATH
	PAGER
	PS1
	PWD
	USER


## Aliases

|Command                 	|Explanation                    |
|---------------------------|-------------------------------|
|alias         				|`Show aliases`                 |
|alias showContent="ls -lha"|`Create new alias`             |
|unalias showContent        |`Remove alias` 	            |


## Directories and link

> #### Symbols explonations

|Symbol                 |Explanation                    |
|-----------------------|-------------------------------|
|.                      |`This directory`               |
|\.\.                   |`Parent directory`             |
|/                      |`Root`                         |
|~                      |`Home`					        |
|{}                     |`Multiple operator`		    |

> #### Commands for manipulation

|Command                 |Explanation                   |
|-----------------------|-------------------------------|
|cd /home/ecneb         |`Change directory`             |
|mkdir test             |`Create directory`             |
|mkdir -p t1/t2/t3      |`Create directory recursively` |
|rmdir test             |`Remove directory`				|
|rmdir -p t1/t2/t3      |`Remove directory recursively` |
|ls -s /tmp/m.txt m     |`Create link in current dir`   |
|ls  					|`Show directory contents`      |
|ls -l      			|`Show in list format`          |
|ls -a      			|`Show hidden files`            |
|ls -t     				|`Sort by time`                 |
|ls -h      			|`Human readable file size`     |
|ls -r      			|`Reverse order`                |
|ls -Z      			|`Show SELinux context`         |
|tree   				|`Show contents in graph format`|
|tree -d      			|`Show only directories`        |
|touch file_{01..100}  	|`Create 100 files`	            |
|echo {1..10..3}     	|`Print range 1 4 7 10`         |
|echo {A..Z}    		|`Print letters from A to Z`    |


## Permissions

> #### Example

|Type|User permissions|Group permissions|Other permissions|Number of elments|    Owner|    Group|   Size|    Date creation|    Time creation|   Name|
|-|---|---|---|-|-----|-----|----|-----|-----|----|
|d|rwx|r-x|r-x|2|ecneb|ecneb|4096|Jan 9|03:25|test|

> #### Type of files

|Symbol                 |Explanation                    |
|-----------------------|-------------------------------|
|-                      |`Regular file`		            |
|d                      |`Directory`			        |
|l                      |`Symbolic link`                |

> #### Type of permissions

|Symbol                 |Explanation                    |
|-----------------------|-------------------------------|
|r                      |`Read`		                    |
|w                      |`Write`			            |
|x                      |`Execute`                      |

> #### List of options

|Octal|Binary|String|Description       |
|-----|------|------|------------------|
|0    |0	 |---   |No permissions    |
|1    |1	 |--x   |Execute only      |
|2    |10    |-w-   |Write only        |
|3    |11	 |-wx   |Write execute     |
|4    |100	 |r--   |Read only         |
|5    |101   |r-x   |Read execute      |
|6    |110	 |rw-   |Read write        |
|7    |111   |rwx   |Read write execute|

> ####  Calculation of default permissions

| 		  			|Directory|File|
|-------------------|---------|----|
|Base permissions  	|777	  |666 |
|Substract umask  	|-022	  |-022|
|Creation permission|755	  |644 |

> #### Commands for manipulation

|Command                      						 |Explanation                      			   |
|----------------------------------------------------|---------------------------------------------|
|chmod u-r,g+w,o=rwx test.txt 				   	     |`Change permission via Strings`  			   |
|chmod -R u-r,g+w,o=rwx test.txt 			   	     |`Change permission via Strings recursively`  |
|chmod 777 test.txt           						 |`Change permission via Binaries` 			   |
|chown ecneb 	test.txt        					 |`Change owner of file`	       			   |
|chgroup -R ecneb www        					 	 |`Change group of dir content`    			   |
|chcon system_u:object_r:httpd_config_t:s0 httpd.conf|`Change context` 				   			   |
|restorecon httpd.conf           					 |`Restore context`    			   			   |
|umask -S  	           								 |`Show default permissions`	   			   |
|umask -S 0022  	           						 |`Set temp default permissions`   			   |

> #### ACL(Access control list)

|Command                      						 |Explanation   		     			  |
|----------------------------------------------------|----------------------------------------|
|getfacl aclfile.txt 								 |`Show acl for file` 					  |
|ls -l 												 |`The + symbol shows that there is a acl`|
|setfacl -m user::rwx aclfile 				         |`Set facl for all users` 				  |
|setfacl -m group::rwx aclfile 				         |`Set facl for all groups` 			  |
|setfacl -m mask::rwx aclfile 				         |`Set facl for mask`					  |
|setfacl -m other::rwx aclfile 				         |`Set facl for others`					  |
|setfacl -m user:root:rwx aclfile 			         |`Set facl for user root`				  |
|setfacl -m user:ecneb:rwx aclfile 			         |`Set facl for user ecneb`				  |
|setfacl -m group:sudo:rwx aclfile			         |`Set facl for group sudo`				  |
|setfacl -m group:marketing:rwx aclfile		         |`Set fac; for group marketing`		  |
|setfacl -R -m group:accounting:rwx dir1 			 |`Set default ACL` 			 		  |
|setfacl -d -m group:accounting:rwx dir1 		     |`Set ACL for any future files` 		  |
|setfacl -x group:root acldeldir/	 				 |`Delete group` 					      |
|setfacl -x root acldeldir/ 			 			 |`Delete user` 						  |
|setfacl -k acldeldir/ 				 				 |`Delete defaults` 					  |
|setfacl -b acldeldir/ 				 				 |`Delete everything` 					  |
|getfacl file1.txt | setfacl --set-file=- file2.txt  |`Copy ACL`  			 				  |
|getfacl -c file1.txt > acls.txt 					 |`Save ACL to file` 	 		 		  |
|setfacl -M acls.txt file.txt 		  				 |`Assigning via file` 	 		 		  |


## User management

- Linux supports many different users logged in at the same time.
- And administrator can add multiple users to a group and then give that group specific access to resources.
- Every user has a user name and a numeric user ID.
- Every group has a group name and a numeric group ID.
- Every user belongs to only one primary group.
- In linux every user has their own primary group with their name. (or the group is called users)

> #### hash types ($1$FSA5456F.sdsaFDW423)

|Value      		    |Hash 	         |
|-----------------------|----------------|
|1 						|MD5  			 |
|2a or 2y 			    |Blowfish 		 |
|5 						|SHA256 		 |
|6 						|SHA512 		 |

> #### less /etc/passwd

|User name|Password encoding type|Numeric user id (0-999 = System accounts) (1000+ = User accounts)|Primary group id number|Comment field|Home directory|Default login shell|
|---------|----------------------|-----------------------------------------------------------------|-----------------------|-------------|--------------|-------------------|
|root     |x 				     |0 															   |0 					   |root 		 |/root 		|/bin/bash  		|	

> #### less /etc/shadow

|User name|Password hash						|Number of days between 1/1/1970|Number of days beffore password can change|Number of days before password be changed|Number of days to warn before password expires|Number of days after the password expires that account is disabled|Number of days between 1/1/1970 and the date the account was disabled|Reserved for future|
|---------|-------------------------------------|-------------------------------|------------------------------------------|-----------------------------------------|----------------------------------------------|------------------------------------------------------------------|---------------------------------------------------------------------|-------------------|
|grant     |$1$E09Egacf$asd4564dwqF.ADW465fds/ 	|17176 							|0 					   					   |99999 		 							 |7 											|7  															   |2																	 | 					 |	
	
> #### less /etc/group

|Group name|Password encoding type or placeholder for password in /etc/gshadow|Group id number|Group members|
|----------|------------------------------------------------------------------|---------------|-------------|
|users     |x 				     											  |100		      |grant,ted	|	

> #### less /etc/gshadow

|Group name, Has to match name in /etc/group|Password hash			|Group admin, can change group password, can add memebers|Group members, can change to the group without a password|
|-------------------------------------------|-----------------------|--------------------------------------------------------|---------------------------------------------------------|
|accounting    								|$1$FSA5456F.sdsaFDW423 |grant											 	     |ecneb,bob												   |	

> #### vim /etc/security/pwquality.conf (Password credit system)

	difok = 5			-> number of character that must nt be in old password
	minlen = 9			-> minimum size for the new password
	dcredit = 1			-> maximum credit for using digits
	ucredit = 1			-> maximum credit for using uppercase charaters
	lcredit = 1			-> maximum credit for using lowercase charaters
	ocredit = 1			-> maximum credit for using other characters
	minclass = 1			-> min number of required classes of chaters
	maxrepeat = 0			-> maximum number of consecutive same characters
	gecoscheck = 0			-> check for words from the comment field longer than 3 chracter in straight or reversed form
	maxclassrepeat = 0		-> maximum nubmer if consecutive character of the same class

> #### User management commands (most of the changes require password change or relogin)

|Command      		    					|Explanation          																						         |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
|sudo pwconv           						|`enable shadow suite for users`																			         |
|sudo unpwconv 								|`disable shadow suite for users (this way we will be able to see the hash in passwd just x)`  				         |
|sudo grpconv								|`enable shadow suite for groups`																			         |
|sudo ungrpconv 							|`disable shadow suite for groups (this way we will be able to see the hash in group not just x)`			         |
|sudo authconfig --passalgo=sha512 --update |`change hash type to sha512` 																				         |
|cat /etc/login.defs  					    |`check if it has been changed to sha512` 																	         |
|change -d 0 ecneb							|`Number of days bettween 1/1/1970 and when password last changed. Setting to 0 forces password change on next login`|
|change --expiredate 2017-10-25 ecneb		|`The date that user's account will expire` 																		 |
|change --inactive 7 ecneb					|`Number of days inactivity after password expiration before the account is locked` 							     |
|change -m ecneb							|`Minimum number of days bettween password changes. Set to 0 user may change password at any time`					 |
|change -M ecneb							|`Maximum nubmer of days password is valid` 																		 |
|change -W ecneb							|`Number of days of warning before a password change is required`													 |
|sudo adduser ecneb 						|`Add user via wizard` 																							 	 |
|sudo useradd ecneb  						|`Add user` 																										 |
|sudo useradd -m ecneb  					|`Add user and create home directory` 																			     |
|sudo userdel ecneb 						|`Delete user`																					  					 |
|sudo usermod -L ecneb						|`Lock user account`																							     |
|sudo usermod -U ecneb  					|`Unlock user account`																								 |
|sudo passwd ecneb 							|`Set password for user ecneb`																						 |
|sudo groupadd -g 1050 accounting 	 		|`Create group with ID`																								 |
|sudo groupmod -g 1051 accounting 			|`Change group id on group accounting`																				 |
|sudo gpasswd -a grant accounting   		|`Add grant to the group accounting`																				 |
|sudo groupdel accounting 					|`Delete group accountding`																							 |
|sudo gpasswd accounting 		 			|`Add password to the group`																				         |

## Switch user & sudoers

|Command      		    |Explanation          			   |
|-----------------------|----------------------------------|
|sudo command           |`Run command as root` 		       |
|sudo -u root command   |`Run command as root` 		       |
|sudo -u ecneb command  |`Run as ecneb` 				   |
|sudo -s                |`Start shell as root` 			   |
|sudo su                |`Switch to the super user account`|
|sudo su ecneb         	|`Switch to the ecneb account`	   |
|usermod -aG sudo ecneb	|`Make ecneb a sudoer` 			   |


## Deleting, copying, moving, renaming, compress and creating archives

|Command              		   |Explanation                              |
|------------------------------|-----------------------------------------|
|rm main.txt 				   |`Remove file`   						 |
|rm -rf testDir 			   |`Remove folder recursevly` 				 |
|rm ./testDir/* 			   |`Remove everything what is inside folder`|
|cp ./testDir/main.txt ../dir  |`Copy file`   							 |
|cp ./testDir/* ../ 		   |`Copy everything what is inside folder`  |
|mv ./testDir/main.txt ../dir  |`Move file`  							 |
|mv ./testDir/* ../ 		   |`Move everything what is inside folder`  |
|mv main.txt test.txt 		   |`Rename file`  							 |
|zip test.txt 				   |`Zip file`	  							 |
|zip -r testDir 			   |`Zip file recursevly`  					 |
|unzip testDir 				   |`Unzip folder`  					  	 |
|unzip test.txt				   |`Unzip file`  							 |
|tar -cf testDir.tar testDir   |`Compress directory` 					 |	 
|tar -tf testDir.tar 		   |`List compress file contents` 			 |
|tar -xf testDir.tar		   |`Uncompress directory` 					 |


## Find and locate files

|Command              		   |Explanation                              	  |
|------------------------------|----------------------------------------------|
|find . -name test.txt		   |`Find test.txt in current dir`   	          |
|find . -iname test.txt		   |`Find test.txt in current dir and ignore case`| 
|find . -size +9k			   |`Find files bigger than 9 kilobytes` 	 	  |
|find . -size +9M			   |`Find files bigger than 9 megabytes` 		  |
|find . -size +9G			   |`Find files bigger than 9 gigabytes` 		  |
|find . -mtime +1			   |`Find files created 2 days ago`   			  |
|find . -mmin +59			   |`Find files created 1 hour ago`   			  |
|locate test.txt			   |`Find file test.txt`						  |
|updatedb 					   |`Update indecies`   					      |


## Reading files

|Command              			  |Explanation                          			  |
|---------------------------------|---------------------------------------------------|
|nl test.sh			 		      |`Display scripts with line numbering`			  |
|cat test.txt		 			  |`Display cotents of file`   		    			  |
|more test.txt		 			  |`Browse to the file`   			    			  |
|less test.txt		 			  |`Browse to the file`   			    			  |
|head test.txt		 			  |`Output the beginning of the file`   			  |
|tail test.txt		 			  |`Output the ending of the file`      			  |
|tail -f test.txt	 			  |`Watch file changes` 							  |  
|watch more test.txt 			  |`Watch file changes with any command`			  |
|jq employee.json 				  |`Pretty format json`								  |
|jq '.' employee.json 			  |`Pretty format json at root level` 				  |
|jq '.workers' employee.json 	  |`Pretty format json at workers level`			  |
|jq '.workers.name' employee.json |`Pretty format json at workers level (nested name)`|


## File editors

> #### Nano

	nano
	nano test.txt

|Keys				 		 |Explanation 							             |
|----------------------------|---------------------------------------------------|
|^G    (F1)      	 		 |Display this help text							 |
|^X    (F2)      	 		 |Close the current file buffer / Exit from nano	 |
|^O    (F3)    		 		 |Write the current file to disk					 |
|^R    (F5)      	 		 |Insert another file into the current one			 |
|^W    (F6)      	 		 |Search forward for a string or a regular expression|
|^\    (M-R)     	 		 |Replace a string or a regular expression			 |
|^K    (F9)       	 		 |Cut the current line and store it in the cutbuffer |
|^U    (F10)     	 		 |Uncut from the cutbuffer into the current line	 |
|^J    (F4)      	 		 |Justify the current paragraph						 |  
|^T    (F12)   		 		 |Invoke the spell checker, if available			 |
|^C    (F11)    	 		 |Display the position of the cursor				 |
|^_    (M-G)    	 		 |Go to line and column number						 |
|M-U           		 		 |Undo the last operation							 |
|M-E            	 		 |Redo the last undone operation					 |
|M-A   (^6)      	 		 |Mark text starting from the cursor position		 |
|M-6   (M-^)     	 		 |Copy the current line and store it in the cutbuffer|
|M-]             	 		 |Go to the matching bracket						 |
|M-W   (F16)     	 		 |Repeat the last search							 |
|M-Arrow up             	 |Search next occurrence backward					 |
|M-Arrow down             	 |Search next occurrence forward					 |
|^B    (Left arrow)       	 |Go back one character								 |
|^F    (Right arrow)       	 |Go forward one character							 |
|^Left arrow    (M-Space) 	 |Go back one word									 |
|^Right arrow    (^Space)  	 |Go forward one word								 |
|^A    (Home)    	 		 |Go to beginning of current line					 |
|^E    (End)     	 		 |Go to end of current line							 |
|^R + ^X    		 		 |Execute command									 |	
|^R + ^T    		 		 |To file											 |
|^R + M-F    		 		 |New Buffer										 |
|M-, 				 		 |Next Buffer										 |
|M-, 				 		 |Previous Buffer									 |
|M-Shift A 			 		 |Select mounted									 |
|M-Shift 6 			 		 |Copy												 |
|^U  				 		 |Pase												 |
	
> #### Vi		

	vi
	vi test.txt

|Keys				  |Explanation 							  |
|---------------------|---------------------------------------|
|k 					  |Up one line							  |
|j 					  |Down one line						  |
|h 					  |Left one character	   				  |
|l 					  |Right one character					  |	
|w 					  |Right one word						  |
|b 					  |Geft one word						  |
|^ 					  |Go to the begging of the line		  |
|$ 					  |Go to the end of the line			  |
|i 					  |Insert at the cursor position		  |
|a 					  |Append after the cursor position		  |
|v 					  |Visual mode							  |
|esc 				  |Escape from insert mode				  |
|> 					  |Indent inside in visual mode			  |
|< 					  |Indent outside in visual mode		  |
|x 					  |Delete character						  |
|dd 				  |Delete line							  |
|y 					  |Copy									  |
|yy 				  |Copy current line					  |
|p 					  |Paste the most recent cut or copyd text|
|cw 				  |Change the current word				  |
|u 					  |Undo and redo						  |
|/Word				  |Search for word						  |
|n 					  |Search next							  |
|N 					  |Search previous						  |
|:tabedit			  |New tab								  |
|g t 				  |Next tab								  |
|g T 		          |Previous tab							  |
|:vsp 			   	  |Vertical split						  |
|^w, h		          |Choose left							  |
|^w, L		          |Choose right							  |
|^w, q				  |Close split							  |
|:%d				  |Select and delete all lines			  |
|:%y				  |Select and copy all lines			  |
|:set nu			  |Show line numbers					  |
|:set nonu			  |Remove line number					  |
|:2		   			  |Go to line number					  |
|:w					  |Create & save file					  |
|:e 				  |Edit file							  |
|:w! 		   		  |Forces the file to be saved			  |
|:q 		   		  |Quit									  |
|:q!   				  |Quit without saving changes			  |
|:wq! 				  |Write and quit						  |
|:s/foo/bar			  |Replace first match in line			  |
|:s/foo/bar/g		  |Replace all matches in line			  |
|:%s/foo/bar/g	      |Replace everything in file			  |


## Sort, count, find, output and diff file

|Command              		   |Explanation                    |
|------------------------------|-------------------------------|
|wc -l numbers.xls		   	   |`Prints the number of line`	   |
|sort -r numbers.xls		   |`Sort by reverse order` 	   |
|sort -u numbers.xls 		   |`Sort unique`				   |
|sdiff numbers.xls months.xls  |`Show diff`					   |
|grep -i dog numbers.xls       |`Find by name ignore case` 	   |
|grep -c dog numbers.xls 	   |`Count number of occurrences`  |
|grep -v dog numbers.xls 	   |`Negate`					   |
|ls -l > main.txt 			   |`Send output to file` 		   |
|ls -l >> test.txt 			   |`Send output to file, append`  |


## Wildcards

|Wildcard      |Explanation                    	   |
|--------------|-----------------------------------|
|*			   |`Matches zero or more characters`  |
|?			   |`Matches exacly one character` 	   |
|[[:alpha:]]   |`Only alpha's` 					   |
|[[:alnum:]]   |`Only alnum's`					   |
|[[:digit:]]   |`Only digit's`					   |
|[[:lower:]]   |`Only lower's`					   |
|[[:space:]]   |`Only space's`					   |
|[[:upper:]]   |`Only uppers's`					   |

Examples: *.txt, a*, a*.txt, ?.txt, a?, a?.txt, ca[nt]*, [!aeio]*


## Transferring and Copying Files over the Network

|Command       																  												|Explanation                        |
|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
|ping 192.168.99.100:8080													  												|`send packets to hosts`            |
|telnet 192.168.99.100 8080													  												|`interface to TELNET protocol`     |
|wget 127.0.0.1/main.txt													  												|`Connect via ssh`                  |
|curl 'http:/example.com'																									|`Simple GET request`               |
|curl -v 'http:/example.com'																							    |`Show response headers`            |
|curl -o output.html 'http:/example.com'																					|`Send request to output`           |
|curl -XPOST -d 'name=John&surname=Doe' 'http:/example.com'																	|`Send form data`                   |
|curl -XPUT -d '{"name":"John","surname":"Doe"}' 'http:/example.com'														|`Send JSON`                        |
|curl -XPOST -H 'Authorization: Bearer test' -H 'Content-type: application/json' -d '{"name": "ecneb"}' 'http:/example.com' |`Using headers`                    |
|curl -F 'img_avatar=@/home/petehouston/hello.txt' -F 'img_profile=@/home/petehouston/hello.txt' 'http:/example.com'		|`Sending files`                    |
|ssh ecneb@127.0.0.1 														  												|`Connect via ssh` 			        |
|exit 				 														  												|`Exit from ssh` 					|
|scp ecneb@127.0.0.1:/home/ecneb/Downloads/test/docker-compose.yml /home/ecneb												|`Copy from server to local PC` 	|
|scp /home/ecneb/Desktop/test.zip ecneb@127.0.0.1:/home/ecneb/Downloads  	  												|`Copy from local PC to server`	    |
|sftp ecneb@127.0.0.1 													      												|`Connect via sftp` 				|
|bye 																		  												|`Exit from sftp` 				    |
|get 																		  												|`Download file` 					|
|put 																		  												|`Upload file` 					    |
|rm 																		  												|`Remove file` 					    |


## Package Managers and Repositories

The software can be delivered in tree primary ways:
- Source
- Binary
- Bundle (Package)

		nano-2.3.1.el7.x86_64.rpm 
		---- ----- --- ------ ---
		  |    |    |    |     |
		  |    |    |    |     ------ Type
		  |    |    |    ------------ Architecture
		  |    |    ----------------- Distribution
		  |    ---------------------- Version
		  --------------------------- Name

- Redhat CentOS Fedora uses RPM and YUM Package Managers
- Debian and Ubuntu uses APT DPKG	

|Command       		  |Explanation                       		   |
|---------------------|--------------------------------------------|
|cat /etc/*-release   |`Getting distribution`     				   |
|uname -m 			  |`Getting architecture`     		 		   |

|URL Package repositories 				 |
|----------------------------------------|
|https://www.rpmfind.net/  				 |
|https://packages.ubuntu.com/		  	 |
|https://www.debian.org/distrib/packages |

> #### Debian and Ubuntu (apt, dpkg)		

|Command  							      		  |Explanation                       		   |
|-------------------------------------------------|--------------------------------------------|
|apt search nmap 							      |`Search every where even in description`    |
|apt-get download nmap 							  |`Only download nmap` 					   |
|apt-get install nmap 							  |`Download and install nmap` 				   |
|apt show nmap 									  |`Showing information about nmap` 		   |
|apt-get update 								  |`Get update list of packages` 			   |
|apt-get upgrade 								  |`Update packages` 						   |
|apt list --installed 							  |`Show installed packages` 				   |
|apt list --installed nmap 						  |`Show if nmap is installed` 				   |
|apt-mark hold nmap 							  |`Mark nmap as dont update` 				   |
|apt-mark unhold nmap 							  |`Remove flag dont update` 				   |
|apt remove nmap 								  |`Remove nmap` 						   	   |
|apt purge nmap 								  |`Remove nmap and conf files` 			   |
|dpkg -L nmap 									  |`Check if nmap is installed`				   |
|wget http://l.org/libcrypt1_4.4.18-4ub1_amd64.deb|`Download package manually` 				   |
|dpkg -c libcrypt1_4.4.18-4ubuntu1_amd64.deb 	  |`Show depencies for package`				   |
|dpkg -i libcrypt1_4.4.18-4ubuntu1_amd64.deb 	  |`Install package` 				   		   |
|dpgk -r nmap 								      |`Remove package`			 				   |
|dpgk --info libcrypt1_4.4.18-4ubuntu1_amd64.deb  |`Show info about package` 		           |
|dpgk -S nmap 									  |`Getting package what is using command nmap`|

> #### Redhat CentOS Fedora (yum, rpm)		

|Command 						        		  |Explanation                       		       |
|-------------------------------------------------|------------------------------------------------|
|yum search nmap 								  |`Search every where even in description`  	   |
|yum install --downloadonly nmap 				  |`Only download nmap`  						   |
|yum install nmap 							      |`Download and install nmap` 					   |
|yum info nmap 									  |`Showing information about nmap` 			   |
|yum check-update 								  |`Get update list of packages`  				   |
|yum update 									  |`Update packages` 							   | 
|yum list installed 							  |`Show installed packages` 				       |
|yum list nmap 									  |`Show if nmap is installed` 				       |
|yum update -x nmap 							  |`Exclude nmap from update` 					   |
|yum versionlock nmap 	 						  |`Making sure that dependecies doest update nmap`|
|yum update nmap 	 							  |`Update only nmap` 							   |
|yum remove nmap 							      |`Remove nmap` 							       |
|yum grouplist 									  |`Show what can be installed as group` 		   |
|yum groupinfo "Basic Web Server" 				  |`Show information about Basic Web Server` 	   |
|yum groupinstall "Basic Web Server"  			  |`Group install Basic Web Server` 			   |
|yum groupremove "Basic Web Server" 			  |`Group remove Basic Web Server` 				   |
|wget https://nmap.org/dist/nmap-7.40-.x86_64.rpm |`Download package manually` 					   |
|rpm -qfRv nmap 								  |`Show depencies for package` 				   |
|rpm -i nmap-7.40-.x86_64.rpm 					  |`Install package` 							   |
|rpm -e nmap 									  |`Remove package` 							   |
|rpm -qlp nmap-7.40-.x86_64.rpm 				  |`Show info about package`  					   |

> #### Installing from source (via Makefile)		

|Command  		      		   |Explanation                       		   |
|------------------------------|-------------------------------------------|
|tar -xf nmap-7.40-.x86_64.rpm |`Extract downloaded package` 			   |
|cd nmap-7.40-.x86_64 		   |`Go to package folder`				       |
|./configure 				   |`Create source files` 				       |
|make 						   |`Run make command to trigger Makefile`     |
|make -n install 			   |`Show what is going to make install` 	   |
|make install 				   |`Install from source via make` 			   |

- [Managing apt packages via terminal GUI](http://manpages.ubuntu.com/manpages/bionic/man8/aptitude-curses.8.html)


## Input Output

|I/O Name 	 		 |Abbreviation	| File Descriptor  |
|--------------------|--------------|------------------|
|Standard input 	 |stdin		    |0				   |
|Standard output 	 |stdout		|1 				   |
|Standard error 	 |stderr		|2				   |

	>  redirects standard output to a file
	>> redirecs standard output to a file by appending 
	<  redirects input from a file to a command

|Command       											 |Explanation                       		   |
|--------------------------------------------------------|---------------------------------------------|
|ls > ls.txt   											 |`Write output to file`     				   |
|ls >> ls.txt  											 |`Append output to file`     		 		   |
|cp -v * ../otherfolder 1>../success.txt 2>../error.txt  |`Write error and success separately to files`|
|cp -v * ../otherfolder &>../logs.txt     			     |`Write everything to one file`			   |
|ls > /dev/null						    			     |`Send to no where`				  		   |


## Shell history

|Command        |Explanation                       			   |
|---------------|----------------------------------------------|
|history	    |`Displays the shell history`      			   |
|!!             |`Repeat the previus command` 				   |
|!N             |`Repeat the command at line number in history |
|!string        |`Repeat the most recent command 			   |

|Keys        |Explanation      |
|------------|-----------------|
|ctrl r      |`Search` 		   |
|ctrl g      |`Cancel search`  |
|tab         |`Auto complete`  |

> #### Customize shell

	vi ~/.bash_history
	vi ~/.history
	vi ~/.histfile

	vi ~/.bashrc
	PS1="MyTestPrompt> "
	PS1="\u@\h \$ "
	source ~/.bashrc
	echo $PS1

|Mappers     |Explanation      					   |
|------------|-------------------------------------|
|\d 		 |Date 							       |
|\H 		 |Host name 					       |
|\n 		 |New line 							   |
|\@ 		 |Current time in 12hour 			   |
|\A 		 |Current time in 24hour 			   |
|\u 		 |Username of the current user 		   |
|\w 		 |Current working directory 		   |
|\W 		 |Basename of current working directory|
|\$ 		 |UID 								   |


## Schedulink task

	* * * * * command to be executed
	- - - - -
	| | | | |
	| | | | ----- Day of week (0 - 7) (Sunday=0 or 7)
	| | | ------- Month (1 - 12)
	| | --------- Day of month (1 - 31)
	| ----------- Hour (0 - 23)
	------------- Minute (0 - 59)

|Command       |Explanation                       |
|--------------|----------------------------------|
|crontab file  |`Install a new crontab from file` |
|crontab -l    |`List crontab jobs`				  |
|crontab -e    |`Edit crontab jobs` 			  |
|crontab -r    |`Remove crontab jobs`			  |


>/etc/crontab is system crontabs file. Usually only used by root user or daemons to configure system wide jobs. All individual user must must use crontab command to install and edit their jobs as described above.

|Directory 		  	 |Description												  |
|--------------------|------------------------------------------------------------|
|/etc/cron.d/ 		 |`Put all scripts here and call them from /etc/crontab file.`|
|/etc/cron.daily/ 	 |`Run all scripts once a day` 								  |
|/etc/cron.hourly/ 	 |`Run all scripts once an hour`							  |
|/etc/cron.monthly/  |`Run all scripts once a month` 							  |
|/etc/cron.weekly/ 	 |`Run all scripts once a week` 							  |

> #### Shortcuts

|Special string 	 |Meaning
|--------------------|---------------------------------|
|@reboot 			 |`Run once, at startup.` 		   |
|@yearly 			 |`Run once a year, “0 0 1 1 *”.`  |
|@monthly 			 |`Run once a month, “0 0 1 * *”.` |
|@weekly 			 |`Run once a week, “0 0 * * 0”.`  |
|@daily				 |`Run once a day, “0 0 * * *”.`   |
|@hourly 			 |`Run once an hour, “0 * * * *”.` |


Example:
touch st.sh

nano file
	* * * * * /home/ecneb/Desktop/st.sh

crontab file


## Multi tasking and processes
		
|Command    	   |Explanation                       															|
|------------------|--------------------------------------------------------------------------------------------|
|ps -e             |`Display all processes` 																	|
|ps -ef            |`Display all processes in full format` 														|
|ps -e --forest    |`Display a processes tree` 																	|
|ps -u username    |`Display user's processes` 																	|
|ps -p 45665 	   |`Display information about the process` 													|
|jobs -l 		   |`Show all jobs in bg` 																		|
|bg %1 			   |`Send task to bg` 																			|
|fg %1 			   |`Send task to fg` 																			|
|kill %1 		   |`Kill task` 																				|
|fg %1 %2 %3 	   |`Send multiple task to fg` 																	|
|bg %1 %2 %3 	   |`Send multiple task to bg` 																	|
|kill %1 %2 %3 	   |`Kill multiple tasks` 																	    |
|disown %5 		   |`Disown task so it will run after session timeout(ssh), then kill is only possible via ps`  |
|bash sleep.sh 	   |`Start in fg` 																				|
|bash sleep.sh &   |`Start in bg` 																				|

|Keys	         |Explanation 			 	    |
|----------------|------------------------------|
|ctrl + Z 		 |`Send to bg and make inactive`|
|ctrl + C 		 |`Close task`				    |

|Command    	   			|Explanation                    |
|---------------------------|-------------------------------|
|tmux		 	   			|`Start new window` 			|
|tmux list-session 			|`List session` 			    |
|tmux attach			    |`Attach to recent` 			|
|tmux attach -t 0			|`Attach by id` 				|
|tmux attach -t mySession	|`Attach by name` 				|
|tmux kill-session 0		|`Kill session by id`			|
|tmux kill-session mySession|`Kill session by name`			|

|Keys				  |Explanation 			  |
|---------------------|-----------------------|
|ctrl + b + ? 		  |`Show help`			  |
|ctrl + q 			  |`Quit help`			  |
|ctrl + b + c 		  |`Start new tab`		  |
|ctrl + b + x 		  |`Close tab`			  |
|ctrl + b + n 		  |`Next tab`			  |
|ctrl + b + p 		  |`Previous tab`		  |
|ctrl + b + 1 		  |`Tab by number`		  |
|ctrl + b + , 		  |`Rename tab`			  |
|ctrl + b + w 		  |`Show tabs`			  |
|ctrl + b + s 		  |`List sessions`		  |
|ctrl + b + & 		  |`Kill session`		  |
|ctrl + b + d 		  |`Detach session`		  |
|ctrl + b + " 		  |`Split vertical`		  |
|ctrl + b + % 		  |`Split horizontal`	  |
|ctrl + b + arrows 	  |`Navigate in split`	  |
|ctrl + b + x 		  |`Close splitted frame` |


## System maintaince

> #### Getting information about the system

|Command 				    	   			|Explanation                       		|
|-------------------------------------------|---------------------------------------|
|ip addr show 	   				   			|`Show ips` 							|
|lscpu			   				   			|`Show cpus` 						    |
|lsusb			   				   			|`Show list of usb devices` 			|
|lspci			   				   			|`Show list of pci devices` 			|
|free -h 		   				   			|`Show free memory` 					|
|df -h  		   				   			|`Show disks` 							|
|du file		   				   			|`Show disk useage of file` 			|
|baobab 		   				   			|`Show disk usage in gui` 				|
|top 			   				   			|`Show processes` 						|
|cat /etc/*-release				  			|`Show OS informations` 				|
|hostnamectl 	   				   			|`Show hostname` 						|
|who 			   				   			|`Show who is logged in`				|
|last 			   				   			|`Login record`							|
|logname 		   				   			|`Who logged in initially`				|
|whoami 		   				   			|`Show who is the currently logged user`|
|id 			   				   			|`Show id of logged user` 				|
|id ecneb 		   				   			|`Show id for specific user` 			|
|groups ecneb 	   				   			|`Show groups of logged user` 			|
|groups ecneb 	   				   			|`Show groups for specific user` 		|
|localectl 									|`Show current local`					|
|localectl set-locale LANG=en_US.utf8 		|`Change locale`						|
|localectl set-keymap us 					|`Change keyboard`						|
|timedatectl 								|`Show current timedatime settings`  	|
|timedatectl set-timezone America/Vencuvar 	|`Set timezone`							|
|timedatectl set-time 23:26:00 				|`Set time`								|
|timedatectl set-time 2019-09-20 			|`Set date`								|
|timedatectl set-time '2019-09-20 23:26:00' |`Set date and time`					|

> #### Uptime, reboot and shutdown

|Command    	   |Explanation                       		|
|------------------|----------------------------------------|
|shutdown -r 10:00 |`Schedule reboot`						|
|shutdown -c 	   |`Cancel scheduled reboot`				|
|shutdown -r now   |`Reboot PC`								|
|shutdown -h now   |`Shutdown PC`							|
|uptime		 	   |`Show how long is the pc running`		|
|				   |`Short uptime - instable OS`		    | 
|				   |`Long uptime  - outdated OS` 		    |

	0.75 = 1 min
	2.14 = 5 min
	0.43 = 15 min

	1.00 = 1 core at 100% 

	higher number - some tasks have to wait
	lower number  - the pc is not running on full capacity

> #### Services

|Command    	      			   |Explanation          	   						 |
|----------------------------------|-------------------------------------------------|
|systemctl --all --state=inactive  |`List all the inactive service` 				 |
|systemctl --all --state=active    |`List all the active services` 				     |
|systemctl disable NetworkManager  |`Disables the named service` 					 |
|systemctl enable NetworkManager   |`Enables the named service` 					 |
|systemctl status NetworkManager   |`Returns the current status of the named service`|
|systemctl start NetworkManager    |`Starts the named service` 						 |
|systemctl restart NetworkManager  |`Restarts the named service` 					 |
|systemctl stop NetworkManager     |`Stops the named service` 						 |
|systemctl mask NetworkManager     |`Disallows any attempts to start` 				 |
|systemctl unmask NetworkManager   |`Allows any attempts to start` 					 |

> #### Logs

|Command 	    	   									|Explanation          	|
|---------------------------------------------------|---------------------------|
|cat /var/log/messages OR cat /var/log/syslog		|`System logs` 		 	    |
|cat /var/log/boot.log OR journalctl -b 			|`Services how they start` 	|
|cat /var/log/secure OR sudo cat /var/log/auth.log 	|`Security logs` 			|


## Disk management

|Command 								    								|Explanation                        				  |
|---------------------------------------------------------------------------|-----------------------------------------------------|
|ls /dev 					  												|`List devices on PC` 								  |
|ls /dev/disk 					  											|`List disks`		 								  |
|blkid 																		|`Show partition block id` 							  |
|fdisk -l 					    											|`List disk on PC` 									  |
|fdisk /dev/sdb 															|`Start disk management` 							  |
|mkfs -t ext4 /dev/sdb1					    								|`Create file system for partition` 				  |
|mount /dev/sdb1 /mnt/external  		   									|`Mount created partition` 							  |
|mount -o loop /path/to/disk1.iso /mnt/disk 								|`Mount iso file` 				    				  |
|umount /mnt/external 														|`Unmount created partition`        				  |
|mount -a 																	|`Mount everything what is fstab`   				  |
|sshfs -o allow_other,default_permissions ecneb@127.0.0.1:/ /mnt/sshtest 	|`Mount ssh endpoint` 								  |
|rsync -a a/ b/ 															|`Backup and sync between disks` 					  |
|rsync -a ecneb@127.0.0.1:/home/ecneb/Desktop/a/ b/ 						|`Backup and sync between remote PC` (remote -> local)|
|rsync -a a/ ecneb@127.0.0.1:/home/ecneb/Desktop/b/ 						|`Backup and sync between remote PC` (local -> remote)|

- [More about disk encryption](https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/)
- [Logical volume Manager - A layer aboce physical disks](https://www.thegeekdiary.com/redhat-centos-a-beginners-guide-to-lvm-logical-volume-manager/)


## Swap

|Command 								    								|Explanation                        				  		     |
|---------------------------------------------------------------------------|----------------------------------------------------------------|
|fallocate -l 1G /swapfile 													|`Create 1GB swap file` 							  		     |
|chmod 600 /swapfile 														|`Set permissions to root` 							   		     |
|mkswap /swapfile 															|`Create swap` 					 					  		     |
|swapon /swapfile 															|`Add swap and to fstab` 		   					  		     |
|swapon --show 																|`Show swap` 										  		     | 
|swapoff -v /swapfile 														|`Remove swap (file and record from fstab has to be removed too)`|

>cat /etc/fstab

|fs								 |mount			 |type |options  |dump |pass|
|--------------------------------|---------------|-----|---------|-----|----|
|/dev/sdba1 					 | /			 |xfs  |defaults |0    |0   |
|UUID=fds789er-dfs4654dsf-dfsd4f6| /mnt/external |ext4 |defaults |0    |0   |
|/swapfile 					     |swap 			 |swap |defaults |0    |0 	|

## Network management

	en p0 s3 
	-- -- --
	|  |  | 
	|  |  -------- Slot s1 s2 s3  
	|  ----------- Bus [p]ci [u]sb
	-------------- Type [e]ther[n]et [w]ir[e]less  

> #### Basics

|Command      			   |Explanation    	   						   |
|--------------------------|-------------------------------------------|
|ip addr 				   |`Information about interfaces and ip`	   |
|ip -4 addr 			   |`Information in ipv4 format`			   |
|ip -6 addr 			   |`Information in ipv6 format`			   |
|ip link set enp0s3 down   |`Turn off interface` 					   |
|ip link set enp0s3 up     |`Turn on interface` 					   |
|ethtool enp0s3 		   |`Detailed information about the interface` |

> #### NetworkManager

|Command    	      									    |Explanation          	   						 |
|-----------------------------------------------------------|------------------------------------------------|
|nm-connecion-editor 									    |`Start NetworkManager GUI` 				     |
|nmcli device 												|`List available devices` 						 |
|nmcli connection 											|`List connected devices` 						 |
|nmcli connection down MyEthernet 							|`Turn off MyEthernet device` 					 |
|nmcli connection up MyEthernet 							|`Turn on MyEthernet device` 					 |
|nmcli connection show ec12d91a-18a6-3a37-8f22-3934f47a6631 |`Show configuration of device with uuid` 		 |
|nmcli connection edit ec12d91a-18a6-3a37-8f22-3934f47a6631 |`Edit configuration of device with uuid` 		 |
|nmcli > describe connection.id 							|`Describe configuration item` 					 |
|nmcli > set connection.id MyEthernet 						|`Set configuration item` 						 |
|nmcli > remove ipv4.addresses 								|`Remove configured item` 						 |
|nmcli > set ipv4.addresses  10.0.2.8/24 					|`Set ipv4 address` 							 |
|nmcli > set ipv4.gateway  10.0.2.1 						|`Set gateway`									 |
|nmcli > set ipv4.dns 10.0.2.1	 							|`Set dns`  									 |
|nmcli > save 												|`Save changes` 								 |
|nmcli radio wifi 											|`Show wifi device` 						     |
|nmcli radio wifi on 										|`Turn on wifi`									 |
|nmcli radio wifi off 										|`Turn off wifi` 								 |
|nmcli dev wifi list 										|`List available networks` 						 |
|nmcli dev wifi connect wifi-name password "wifi-password"  |`Connect to wireless network with password`     |

> #### Firewalld

|Command    	      			   							   |Explanation          	   		  		   |
|--------------------------------------------------------------|-------------------------------------------|
|firewall-config 											   |`Start firewall GUI` 					   |
|firewall-cmd --remove-service=http 						   |`Remove item from firewall via service`    |
|firewall-cmd --add-service=pop3s 							   |`Add item to firewall via service`		   | 
|firewall-cmd --zone=public --add-port=4545/tcp --permanent    |`Add item to firewall via port` 		   | 
|firewall-cmd --zone=public --remove-port=4545/tcp --permanent |`Remove item from firewall via port`	   |
|firewall-cmd --list-all 									   |`Get complete list` 					   |
|firewall-cmd --list-services 								   |`Get list of assigned services` 		   |
|firewall-cmd --list-all-zones 								   |`Get complete list for all zones`		   |
|firewall-cmd --get-zones 									   |`Get list of zones`						   |
|firewall-cmd --get-services 								   |`Get list of services` 					   | 
|firewall-cmd --get-default-zone					  		   |`Get default zone` 						   |
|firewall-cmd --set-default-zone=work     					   |`Set default zone` 						   |
|firewall-cmd --get-active-zones          					   |`Get active zones`						   |
|firewall-cmd --get-zone-of-interface=enp0s3 				   |`Get zone by interface` 				   |
|firewall-cmd --zone=work --add-interface=enp0s3 			   |`Set zone for interface` 				   |	
|firewall-cmd --reload 										   |`Make changes permanent if added via port` |
|firewall-cmd --runtime-to-permanent 						   |`Change runtime configurtion to permanent` |

> #### Netstat and SS

|Command      |Explanation          	|
|-------------|-------------------------|
|ss -tln 	  |`Listening connections` 	|
|ss -tn 	  |`Established connections`|
|netstat -tln |`Listening connections` 	|
|netstat -tn  |`Established connections`|


## Connect To Remote Desktop

Remote Desktop Protocol:
- VNC
- RDP (Recommended)
- NX

Remote CLI protocols:
- SSH (Recommended)
- RLogin
- Telnet

|Command      			   							   |Explanation    	   						       |
|------------------------------------------------------|-----------------------------------------------|
|apt install openssh-server 				    	   |`Install package to be able to connect via shh`|
|apt install xrdp 									   |`Install package to be able to connect via rdp`|
|firewall-cmd --add-service=ssh 					   |`Enable ssh on firewall` 					   |
|firewall-cmd --permament --zone=public --port=3389/tcp|`Enable xrd protocol on firewall` 			   |
|firewall-cmd --reload 								   |`Apply firewall changes` 					   |
|ifconfig 											   |`Show ip address` 							   |


## AWK


## SED

What?
- A stream editor
- Developed in Bell labs
- Command line version of text editor ed

Purpose?
- Simple manipulations on line oriented text files
- Most often used as a filter, often in shell scipts
- It possible to write SED programs

> #### Replace the first line occurrence of the word 'old' with 'new' in the file 'text.txt'

```bash
sed 's/old/new/' text.txt
```

> #### Replace the all occurrence of the word 'old' with 'new' in the file 'text.txt'

```bash
sed 's/old/new/g' text.txt

# Non overlapping behaviour (it replaces one by one) 
# abababababa
# ---b---b---
sed 's/aba/---/g'
```

> #### Replace the all occurrence of the word 'old' with 'new' from input

```bash
sed 's/old/new/g'
```

> #### Get source from 'text.txt' and then store it in 'output.txt'

```bash
sed 's/old/new/g' < text.txt > output.txt
```

> #### Using pipe

```bash
wc text.txt | sed 's/old/new/g'
```

> #### Using regex (find ten, men and replace it with new) in a file called text.txt

```bash
sed 's/[tm]en/new/g' text.txt
```

> #### Put 'the' into prentices '(the)'

```bash 
sed 's/the/(&)/g'
```

> #### Change the order from 'they were' to 'were they'

```bash
sed 's/\(they\) \(were\)/\2 \1/g'
```

> #### Using '-n' flag to hide output

```bash
sed -n 's/old/new/' text.txt
```

> #### Using '-n' flag to hide output and '[' mode to show only changed lines

```bash
sed -n 's/old/new/p' text.txt
```

> #### Specifying multiple commands with '-e'

```bash
sed -e 's/up/UP/' -e 's/down/DOWN/' text.txt
```

> #### Specifying multiple commands with '-f'

```bash
cat > script
s/up/UP/
s/down/DOWN/

sed -f script text.txt
```

> #### Print first line

```bash
sed '1p' text.txt
```

> #### Print last line

```bash
sed '$p' text.txt
```

> #### Print lines from '1' to '3'

```bash
sed '1,3p' text.txt
```

> #### Print lines from 'men' to 'end'

```bash
sed -n '/men/,/up/' text.txt
```

> #### Delete all lines containing 'up'

```bash
sed 'up/d'
```

> #### Delete from 'men' to 'up'

```bash
sed '/men/,/up/d'
```

> #### Insert a line with content of 'up' to the lines which contains 'down'

```bash
sed '/down/ i\up\' text.txt
```

> #### Append a line with content of 'up' to the lines which contains 'down'

```bash
sed '/down/ a\up\' text.txt
```

> #### It replaces the line from 'top' to 'again' with our lines what we specify

```bash
sed '/top/,/again/ c\This just a test\' text.txt
```

> #### It replaces the word 'down' with the content of the file 'down.txt'

```bash
sed '/down/r down.txt' text.txt
```

> #### It saves the lines from '1' to '3' into top.txt

```bash
sed '1,3w top.txt' text.txt
```

> ### Using grouping as a programs

```bash
# Search in lines from 3 to 6 
# Find the word 'marched'
# get the next line
# add ((
# get the next line
# add ))

cat > script
3,6 {
	/marched/ {
		n
		s/^/((/
		n
		s/$/))/
	}
}
```


## Bash programing

Every bash script should start with #!/bin/bash
- #! = Hashbang or Shebang
- /bin/bash = path to the bash executable

We can execute the bash scripts via:
- ./script.sh (chmod +x scripts.sh)
- sh scripts.sh
- bash scripts.sh
- script.sh (script must be in /usr/bin or on the $PATH variable)

> #### String interpretation and variables

```bash
#!/bin/bash

name="ecneb"
echo "hello $name !"
unset $name
```

> #### Command substation

```bash
#!/bin/bash

d=$(pwd)
echo $d
```

> #### Working with numbers

|Command      			   			   |Explanation    	   					  |
|--------------------------------------|--------------------------------------|
|((expression))				    	   |`Numbers are placed inside perentesis`|

```bash
#!/bin/bash

d=2
e=$((d+2))
echo $e
((e++))
echo $e
((e--))
echo $e
echo $((e+=5))
echo $((e*=3))
echo $((e/=3))
echo $((e-=3))
```

> #### Grouping

|Command      			   |Explanation    	   					  |
|--------------------------|--------------------------------------|
|()				    	   |`New scope, result will be lost`	  |
|{}				    	   |`Same scope, just grouping`           |

	a=1 		a=1
	(			{
	a=2 		a=2
	)			}
	echo $a 	echo $a
	//prints 1    //prints 2

> #### Comparing values

|Command      			   |Explanation    	   					  		  |
|--------------------------|----------------------------------------------|
|[[>]] 					   |`For String, where a is greater than b`       |
|[[<]] 					   |`For String, where a is less than b`		  |
|[[<=]] 				   |`For String, where a is less or equal to b`   |
|[[>=]] 				   |`For String, where a is greater or equal to b`|
|[[==]] 				   |`For String, where a is equal to b`           |
|[[!=]] 				   |`For String, where a is not equal to b`		  |
|[[-lt]] 				   |`For Number, where a is less than b`		  |
|[[-gt]] 				   |`For Number, where a is greater than b`		  |
|[[-le]] 				   |`For Number, where a is less or equal to b`   |
|[[-ge]] 				   |`For Number, where a is greater or equal to b`|
|[[-eq]] 				   |`For Number, where a is equal to b` 		  |
|[[-ne]] 				   |`For Number, where a is not equal to b`		  |
|[[&&]] 				   |`Logical and operator`						  |
|[[\|\|]] 				   |`Logical or operator`						  |
|[[!]] 					   |`Logical not operator`						  |
|[[-z]] 				   |`Is null`									  |
|[[-n]] 				   |`Is not null`								  |

```bash
#!/bin/bash

[[ "cat" == "cat" ]]
echo $?
[[ "cat" == "dog" ]]
echo $?

[[ 5 -lt 6 ]]
echo $?

a=""
b="cat"

[[ -z $a && -n $b ]]
echo $?
```

> #### Working with strings

```bash
#!/bin/bash

# Declare options
	declare -l lsString = "ABCdef"
	declare -l usString = "ABCdef"
	declare -r readonly = "A value"

# Concatenation
	a="hello"
	b="world"
	c=$a$b
	echo $c

# Lenght
	echo ${#a}

# Substring (from position 3 to the end)
	d=${c:3}
	echo $d

# Substring (from position 3 to the 4 char)
	d=${c:3:4}
	echo $d
	
# Substring (starting from the end)
	d=${c: -4}
	echo $d

# Replace
	fruit="apple banana banana cherry"
# Replace (it replaces the first banana)
	echo ${fruit/banana/durian}
# Replace (replace all instances of banana)
	echo ${fruit//banana/durian}
# Replace (replaces only if the word is on start )
	echo ${fruit/#apple/durian}
```

> #### Using styles

|Color 			   |Foreground    	   	  |Background 			 |
|------------------|----------------------|----------------------|
|`Black`		   |30					  |40 				     |
|`Red`			   |31					  |41 				     |
|`Green`		   |32					  |42 				     |
|`Zellow`		   |33					  |43 				     |
|`Blue`			   |34					  |44 				     |
|`Magenta`		   |35					  |45 				     |
|`Cyan`			   |36					  |46 				     |
|`White`		   |37					  |47 				     |

|Style 			   |Code    		  |   	  
|------------------|------------------|
|No style 		   |0 				  |
|Bold 			   |1 				  |
|Low intensity     |2 				  |
|Underline 		   |4 				  |
|Blinking 		   |5 				  |
|Reverse 		   |7 				  |
|Invisble 		   |8 				  |

```bash
#!/bin/bash

echo -e '\033[37;40mWhite on Black\033[0m'
echo -e '\033[5;37;40mWhite on Black and blinking\033[0m'

flashered="\033[5;31;40m]"
red="\033[31;40m"
none="\033[0m"
echo -e $flashred"ERROR: "$none$red"Something when wrong."$none
```

> #### Using printf

```bash
#!/bin/bash
printf "Name:\t%s\nID:\t%04d\n" "ecneb" "12"
```

> #### Working with arrays

```bash
#!/bin/bash

# Empty array
	a=()
	echo $a

# Array
	b=("apple", "banana", "cherry")
	echo ${b[@]}

# Add to the end
	b+=("mango")
	echo ${b[@]}

# Add at index 5
	b[5]="kiwi"
	echo ${b[@]}

# Print out the 2 index
	echo ${b[2]}

# Wole array
	echo ${b[@]}

# Last element
	echo ${b[@]: -1}

# Creating assosicate array
	declare -A myarray
	myarray[color]=blue
	myarray["office building"]="HQ West"

	echo ${myarray["office building"]}
	echo ${myarray[color]}
```

> #### Working with files

```bash
#!/bin/bash

echo "Some text" > file.txt
echo "Some text 2" >> file.txt

while read f; do
	echo $f
done < file.txt
```

> #### Using here docs

```bash
#!/bin/bash

ssh -T ecneb@localhost << EOF
echo "The current local working directory is: $PWD"
echo "The current remote working directory is: \$PWD"
EOF

cat << EOF
This is a
multiline
text
string
EOF
```

> #### Controling structure

```bash
#!/bin/bash

n=2
if [ $n -eq 1 ]; then
    echo value of n is 1
elif [ $n -eq 2 ]; then
    echo value of n is 2
else
    echo value of n is other than 1 and 2
fi


a="dog"
case $a in
		cat) echo "Feline";;
		dog|puppy) echo "Canines";;
		*) echo "No match";;
esac
```

> #### Using loops

```bash
#!/bin/bash

# While loop
	i = 0
	while [ $i -le 10 ]
	do
		echo $i
		((i+=1))
	done

# Until loop
	j = 0
	until [ $j -ge 10 ]
	do
		echo $j
		((j+=1))
	done

# For loop
	for k in 1 2 3
	do
		echo $k
	done

	for t in {1..100}
	do
		echo $t
	done

	arr=("apple", "banana", "cherry")
	for q in ${arr[@]}
	do
		echo $q
	done		
```

> #### Using functions

```bash
#!/bin/bash
function greet {
	echo "Hi there $1 nice $2"
}

echo "And now a greeting"
greet ecneb Morning

function numberthings {
	for f in $@
	do
		echo  $f
		((i+=1))
	done
}

numberthings $(ls)
```

> #### Working with arguments

```bash
#!/bin/bash
echo $1
echo $2

echo "There were $# arguments"		
```
- ./script.sh Apple Orange

> #### Working with flags

```bash
#!/bin/bash
while getopts u:p option
	do
	case $option in
		u) user=$OPTARG;;
		p) pass=$OPTARG;;
		?) echo "I dont know what $OPTARG is??";;
	esac
done

echo "User: $user / Password: $pass"
```

- ./script.sh -u ecneb -p password


> #### Getting input from the user

```bash
#!/bin/bash

# Newline prompt
	echo "What is your name"
	read name

# Hidden prompt
	echo "What is your password"
	read -s pass

# Inline prompt
	read -p "What is your favorite animal?" animal

# Select list
	select animal in "cat" "dog"
	do
		echo "You selected $animal"
		break
	done

echo $name
echo $pass
echo $animal

# Act on answer
	select option in "cat" "dog"
	do
		case $option in 
			cat) echo "cats like to sleep";;
			dog) echo "dogs like to play"
			*) echo "Im not sure what is this"
		esac
	done

# Force answer
	read -p "Favorite animal?"
	while [[ -z "$a"]]; do
		read -p "I need an answers" a
	done
	echo "$a was selected "

# Default answer
	read -p "Favorite animal? [cat]"
	while [[ -z "$a"]]; do
		a="cat"
	done
	echo "$a was selected"
```

> #### Using trap, to handling exit or termination

|Command      			   |Explanation    	   					  |
|--------------------------|--------------------------------------|
|kill -l		    	   |`List of signal options`			  |

```bash
#!/bin/bash
trap "echo just got int; exit" INT
trap "echo you cannot quit now" QUIT

while
true
do
	echo looping
        du -m * 2>/dev/null     
        echo sleeping
        sleep 5
done
```

> #### Debugging

|Command      			   		  |Explanation    	   					  			    |
|---------------------------------|-----------------------------------------------------|
|bash -x script.sh		    	  |`Echoing commands after processing`			  	    |
|bash -n script.sh		    	  |`Do not execute script, just check for syntax errors`|
|ls \| tee my.log \| grep -i file |`Catch outpout from pipe and save it to file`		|
|source script.sh 		   		  |`Making all variables and function available in bash`|
|export a 		 		   		  |`Export variable for another bash window`			|
|export -f myFunction	   		  |`Export function for another bash window`			|
|export 		 		   		  |`List of exported items`							    |

|Script variables	   |Explanation    	   						  |
|----------------------|------------------------------------------|
|set -u		    	   |`Enables reporting of unset variables`	  |
|set +u		    	   |`Disables reporting of unset variables`	  |
|set -x		    	   |`Activating tracing`			  		  |
|set +x		    	   |`Deactivating tracing`			 		  |


## Server management

