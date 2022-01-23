
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

>https://explainshell.com/
	
	man ls
	ls --help

	ls
	cd
	pwd
	touch
	echo
	clear
	exit


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


## Directories and link

> #### Symbols explonations

|Symbol                 |Explanation                    |
|-----------------------|-------------------------------|
|.                      |`This directory`               |
|\.\.                   |`Parent directory`             |
|/                      |`Root`                         |
|~                      |`Home`					        |
|{}                     |`multiple operator`		    |

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
|touch file_{01..100}  	|`create 100 files`	            |
|echo {1..10..3}     	|`print range 1 4 7 10`         |
|echo {A..Z}    		|`print letters from A to Z`    |


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

|Command                      						 |Explanation                      |
|----------------------------------------------------|---------------------------------|
|chmod u-r,g+w,o=rwx test.txt 				   	     |`Change permission via Strings`  |
|chmod 777 test.txt           						 |`Change permission via Binaries` |
|chown ecneb 	test.txt        					 |`Change owner of file`	       |
|chgroup -R ecneb www        					 	 |`Change group of dir content`    |
|chcon system_u:object_r:httpd_config_t:s0 httpd.conf|`Change context` 				   |
|restorecon httpd.conf           					 |`Restore context`    			   |
|umask -S  	           								 |`Show default permissions`	   |
|umask -S 0022  	           						 |`Set temp default permissions`   |


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

|Command             |Explanation                          |
|--------------------|-------------------------------------|
|cat test.txt		 |`Display cotents of file`   		   |
|more test.txt		 |`Browse to the file`   			   |
|less test.txt		 |`Browse to the file`   			   |
|head test.txt		 |`Output the beginning of the file`   |
|tail test.txt		 |`Output the ending of the file`      |
|tail -f test.txt	 |`Watch file changes` 				   |  
|watch more test.txt |`Watch file changes with any command`|


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
|wget 127.0.0.1/main.txt													  												|`Connect via ssh`                  |
|curl 'http:/example.com'																									|`Simple GET request`               |
|curl -o output.html 'http:/example.com'																					|`Send request to output`           |
|curl -X "POST" -d "name=John&surname=Doe" 'http:/example.com'																|`Send form data`                   |
|curl -X "PUT" -d "{"name":"John","surname":"Doe"}" 'http:/example.com'														|`Send JSON`                        |
|curl -XPOST -H 'Authorization: Bearer test' -H "Content-type: application/json" -d '{"name": "ecneb"}' 'http:/example.com' |`Using headers`                    |
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

	Redhat CentOS Fedora uses RPM and YUM Package Managers
	Debian and Ubuntu uses APT DPKG	

|Command       		  |Explanation                       		   |
|---------------------|--------------------------------------------|
|cat /etc/*-release   |`getting distribution`     				   |
|uname -m 			  |`getting architecture`     		 		   |

|URL Package repositories 				 |
|----------------------------------------|
|https://www.rpmfind.net/  				 |
|https://packages.ubuntu.com/		  	 |
|https://www.debian.org/distrib/packages |

> #### Debian and Ubuntu (apt, dpkg)		

|Command  							      		  |Explanation                       		   |
|-------------------------------------------------|--------------------------------------------|
|apt search nmap 							      |`search every where even in description`    |
|apt-get download nmap 							  |`only download nmap` 					   |
|apt-get install nmap 							  |`download and install nmap` 				   |
|apt show nmap 									  |`showing information about nmap` 		   |
|apt-get update 								  |`get update list of packages` 			   |
|apt-get upgrade 								  |`update packages` 						   |
|apt list --installed 							  |`show installed packages` 				   |
|apt list --installed nmap 						  |`show if nmap is installed` 				   |
|apt-mark hold nmap 							  |`mark nmap as dont update` 				   |
|apt-mark unhold nmap 							  |`remove flag dont update` 				   |
|apt remove nmap 								  |`remove nmap` 						   	   |
|apt purge nmap 								  |`remove nmap and conf files` 			   |
|dpkg -L nmap 									  |`check if nmap is installed`				   |
|wget http://l.org/libcrypt1_4.4.18-4ub1_amd64.deb|`download package manually` 				   |
|dpkg -c libcrypt1_4.4.18-4ubuntu1_amd64.deb 	  |`show depencies for package`				   |
|dpkg -i libcrypt1_4.4.18-4ubuntu1_amd64.deb 	  |`install package` 				   		   |
|dpgk -r nmap 								      |`remove package`			 				   |
|dpgk --info libcrypt1_4.4.18-4ubuntu1_amd64.deb  |`show info about package` 		           |
|dpgk -S nmap 									  |`getting package what is using command nmap`|

> #### Redhat CentOS Fedora (yum, rpm)		

|Command 						        		  |Explanation                       		       |
|-------------------------------------------------|------------------------------------------------|
|yum search nmap 								  |`search every where even in description`  	   |
|yum install --downloadonly nmap 				  |`only download nmap`  						   |
|yum install nmap 							      |`download and install nmap` 					   |
|yum info nmap 									  |`showing information about nmap` 			   |
|yum check-update 								  |`get update list of packages`  				   |
|yum update 									  |`update packages` 							   | 
|yum list installed 							  |`show installed packages` 				       |
|yum list nmap 									  |`show if nmap is installed` 				       |
|yum update -x nmap 							  |`exclude nmap from update` 					   |
|yum versionlock nmap 	 						  |`making sure that dependecies doest update nmap`|
|yum update nmap 	 							  |`update only nmap` 							   |
|yum remove nmap 							      |`remove nmap` 							       |
|yum grouplist 									  |`show what can be installed as group` 		   |
|yum groupinfo "Basic Web Server" 				  |`show information about Basic Web Server` 	   |
|yum groupinstall "Basic Web Server"  			  |`group install Basic Web Server` 			   |
|yum groupremove "Basic Web Server" 			  |`group remove Basic Web Server` 				   |
|wget https://nmap.org/dist/nmap-7.40-.x86_64.rpm |`download package manually` 					   |
|rpm -qfRv nmap 								  |`show depencies for package` 				   |
|rpm -i nmap-7.40-.x86_64.rpm 					  |`install package` 							   |
|rpm -e nmap 									  |`remove package` 							   |
|rpm -qlp nmap-7.40-.x86_64.rpm 				  |`show info about package`  					   |

> #### Installing from source (via Makefile)		

|Command  		      		   |Explanation                       		   |
|------------------------------|-------------------------------------------|
|tar -xf nmap-7.40-.x86_64.rpm |`extract downloaded package` 			   |
|cd nmap-7.40-.x86_64 		   |`go to package folder`				       |
|./configure 				   |`create source files` 				       |
|make 						   |`run make command to trigger Makefile`     |
|make -n install 			   |`show what is going to make install` 	   |
|make install 				   |`install from source via make` 			   |

[Managing apt packages via terminal GUI](http://manpages.ubuntu.com/manpages/bionic/man8/aptitude-curses.8.html)


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
|ls > ls.txt   											 |`write output to file`     				   |
|ls >> ls.txt  											 |`append output to file`     		 		   |
|cp -v * ../otherfolder 1>../success.txt 2>../error.txt  |`write error and success separately to files`|
|cp -v * ../otherfolder &>../logs.txt     			     |`write everything to one file`			   |
|ls > /dev/null						    			     |`send to no where`				  		   |


## Shell history

|Command       |Explanation                       |
|--------------|----------------------------------|
|history	   |`dispplays the shell history`     |

	vi ~/.bash_history
	vi ~/.history
	vi ~/.histfile


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
|crontab file  |`install a new crontab from file` |
|crontab -l    |`list crontab jobs`				  |
|crontab -e    |`edit crontab jobs` 			  |
|crontab -r    |`remove crontab jobs`			  |


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
|jobs -l 		   |`show all jobs in bg` 																		|
|bg %1 			   |`send task to bg` 																			|
|fg %1 			   |`send task to fg` 																			|
|kill %1 		   |`kill task` 																				|
|fg %1 %2 %3 	   |`send multiple task to fg` 																	|
|bg %1 %2 %3 	   |`send multiple task to bg` 																	|
|kill %1 %2 %3 	   |`kill multiple tasks` 																	    |
|disown %5 		   |`disown task so it will run after session timeout(ssh), then kill is only possible via ps`  |
|bash sleep.sh 	   |`start in fg` 																				|
|bash sleep.sh &   |`start in bg` 																				|

|Keys	         |Explanation 			 	    |
|----------------|------------------------------|
|ctrl + Z 		 |`send to bg and make inactive`|
|ctrl + C 		 |`close task`				    |

|Command    	   			|Explanation                    |
|---------------------------|-------------------------------|
|tmux		 	   			|`start new window` 			|
|tmux list-session 			|`list session` 			    |
|tmux attach			    |`attach to recent` 			|
|tmux attach -t 0			|`attach by id` 				|
|tmux attach -t mySession	|`attach by name` 				|
|tmux kill-session 0		|`kill session by id`			|
|tmux kill-session mySession|`kill session by name`			|

|Keys				  |Explanation 			  |
|---------------------|-----------------------|
|ctrl + b + ? 		  |`show help`			  |
|ctrl + q 			  |`quit help`			  |
|ctrl + b + c 		  |`start new tab`		  |
|ctrl + b + x 		  |`close tab`			  |
|ctrl + b + n 		  |`next tab`			  |
|ctrl + b + p 		  |`previous tab`		  |
|ctrl + b + 1 		  |`tab by number`		  |
|ctrl + b + , 		  |`rename tab`			  |
|ctrl + b + w 		  |`show tabs`			  |
|ctrl + b + s 		  |`list sessions`		  |
|ctrl + b + & 		  |`kill session`		  |
|ctrl + b + d 		  |`detach session`		  |
|ctrl + b + " 		  |`split vertical`		  |
|ctrl + b + % 		  |`split horizontal`	  |
|ctrl + b + arrows 	  |`navigate in split`	  |
|ctrl + b + x 		  |`close splitted frame` |


## System maintaince

> #### Getting information about the system

|Command 				    	   			|Explanation                       		|
|-------------------------------------------|---------------------------------------|
|ip addr show 	   				   			|`show ips` 							|
|lscpu			   				   			|`show cpus` 						    |
|lsusb			   				   			|`show list of usb devices` 			|
|lspci			   				   			|`show list of pci devices` 			|
|free -h 		   				   			|`show free memory` 					|
|df -h  		   				   			|`show disks` 							|
|du file		   				   			|`show disk useage of file` 			|
|baobab 		   				   			|`show disk usage in gui` 				|
|top 			   				   			|`show processes` 						|
|cat /etc/*-release				  			|`show OS informations` 				|
|hostnamectl 	   				   			|`show hostname` 						|
|who 			   				   			|`show who is logged in`				|
|last 			   				   			|`login record`							|
|logname 		   				   			|`who logged in initially`				|
|whoami 		   				   			|`show who is the currently logged user`|
|id 			   				   			|`show id of logged user` 				|
|id ecneb 		   				   			|`show id for specific user` 			|
|groups ecneb 	   				   			|`show groups of logged user` 			|
|groups ecneb 	   				   			|`show groups for specific user` 		|
|localectl 									|`show current local`					|
|localectl set-locale LANG=en_US.utf8 		|`change locale`						|
|localectl set-keymap us 					|`change keyboard`						|
|timedatectl 								|`show current timedatime settings`  	|
|timedatectl set-timezone America/Vencuvar 	|`set timezone`							|
|timedatectl set-time 23:26:00 				|`set time`								|
|timedatectl set-time 2019-09-20 			|`set date`								|
|timedatectl set-time '2019-09-20 23:26:00' |`set date and time`					|

> #### Uptime, reboot and shutdown

|Command    	   |Explanation                       		|
|------------------|----------------------------------------|
|shutdown -r 10:00 |`schedule reboot`						|
|shutdown -c 	   |`cancel scheduled reboot`				|
|shutdown -r now   |`reboot PC`								|
|shutdown -h now   |`shutdown PC`							|
|uptime		 	   |`show how long is the pc running`		|
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
|systemctl --all --state=inactive  |`list all the inactive service` 				 |
|systemctl --all --state=active    |`list all the active services` 				     |
|systemctl disable NetworkManager  |`disables the named service` 					 |
|systemctl enable NetworkManager   |`enables the named service` 					 |
|systemctl status NetworkManager   |`returns the current status of the named service`|
|systemctl start NetworkManager    |`starts the named service` 						 |
|systemctl restart NetworkManager  |`restarts the named service` 					 |
|systemctl stop NetworkManager     |`stops the named service` 						 |
|systemctl mask NetworkManager     |`disallows any attempts to start` 				 |
|systemctl unmask NetworkManager   |`allows any attempts to start` 					 |

> #### Logs

|Command 	    	   									|Explanation          	|
|---------------------------------------------------|---------------------------|
|cat /var/log/messages OR cat /var/log/syslog		|`System logs` 		 	    |
|cat /var/log/boot.log OR journalctl -b 			|`Services how they start` 	|
|cat /var/log/secure OR sudo cat /var/log/auth.log 	|`Security logs` 			|


## Disk management

|Command 								    								|Explanation                        				  |
|---------------------------------------------------------------------------|-----------------------------------------------------|
|ls /dev 					  												|`list devices on PC` 								  |
|ls /dev/disk 					  											|`list disks`		 								  |
|blkid 																		|`show partition block id` 							  |
|fdisk -l 					    											|`list disk on PC` 									  |
|fdisk /dev/sdb 															|`start disk management` 							  |
|mkfs -t ext4 /dev/sdb1					    								|`create file system for partition` 				  |
|mount /dev/sdb1 /mnt/external  		   									|`mount created partition` 							  |
|mount -o loop /path/to/disk1.iso /mnt/disk 								|`mount iso file` 				    				  |
|umount /mnt/external 														|`unmount created partition`        				  |
|mount -a 																	|`mount everything what is fstab`   				  |
|sshfs -o allow_other,default_permissions ecneb@127.0.0.1:/ /mnt/sshtest 	|`mount ssh endpoint` 								  |
|rsync -a a/ b/ 															|`backup and sync between disks` 					  |
|rsync -a ecneb@127.0.0.1:/home/ecneb/Desktop/a/ b/ 						|`backup and sync between remote PC` (remote -> local)|
|rsync -a a/ ecneb@127.0.0.1:/home/ecneb/Desktop/b/ 						|`backup and sync between remote PC` (local -> remote)|

- [More about disk encryption](https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/)
- [Logical volume Manager - A layer aboce physical disks](https://www.thegeekdiary.com/redhat-centos-a-beginners-guide-to-lvm-logical-volume-manager/)


## Swap

|Command 								    								|Explanation                        				  		     |
|---------------------------------------------------------------------------|----------------------------------------------------------------|
|fallocate -l 1G /swapfile 													|`create 1GB swap file` 							  		     |
|chmod 600 /swapfile 														|`set permissions to root` 							   		     |
|mkswap /swapfile 															|`create swap` 					 					  		     |
|swapon /swapfile 															|`add swap and to fstab` 		   					  		     |
|swapon --show 																|`show swap` 										  		     | 
|swapoff -v /swapfile 														|`remove swap (file and record from fstab has to be removed too)`|

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
|ip addr 				   |`information about interfaces and ip`	   |
|ip -4 addr 			   |`information in ipv4 format`			   |
|ip -6 addr 			   |`information in ipv6 format`			   |
|ip link set enp0s3 down   |`turn off interface` 					   |
|ip link set enp0s3 up     |`turn on interface` 					   |
|ethtool enp0s3 		   |`detailed information about the interface` |

> #### NetworkManager

|Command    	      									    |Explanation          	   						 |
|-----------------------------------------------------------|------------------------------------------------|
|nm-connecion-editor 									    |`start NetworkManager GUI` 				     |
|nmcli device 												|`list available devices` 						 |
|nmcli connection 											|`list connected devices` 						 |
|nmcli connection down MyEthernet 							|`turn off MyEthernet device` 					 |
|nmcli connection up MyEthernet 							|`turn on MyEthernet device` 					 |
|nmcli connection show ec12d91a-18a6-3a37-8f22-3934f47a6631 |`show configuration of device with uuid` 		 |
|nmcli connection edit ec12d91a-18a6-3a37-8f22-3934f47a6631 |`edit configuration of device with uuid` 		 |
|nmcli > describe connection.id 							|`describe configuration item` 					 |
|nmcli > set connection.id MyEthernet 						|`set configuration item` 						 |
|nmcli > remove ipv4.addresses 								|`remove configured item` 						 |
|nmcli > set ipv4.addresses  10.0.2.8/24 					|`set ipv4 address` 							 |
|nmcli > set ipv4.gateway  10.0.2.1 						|`set gateway`									 |
|nmcli > set ipv4.dns 10.0.2.1	 							|`set dns`  									 |
|nmcli > save 												|`save changes` 								 |
|nmcli radio wifi 											|`show wifi device` 						     |
|nmcli radio wifi on 										|`turn on wifi`									 |
|nmcli radio wifi off 										|`turn off wifi` 								 |
|nmcli dev wifi list 										|`list available networks` 						 |
|nmcli dev wifi connect wifi-name password "wifi-password"  |`connect to wireless network with password`     |

> #### Firewalld

|Command    	      			   							   |Explanation          	   		  		   |
|--------------------------------------------------------------|-------------------------------------------|
|firewall-config 											   |`start firewall GUI` 					   |
|firewall-cmd --remove-service=http 						   |`remove item from firewall via service`    |
|firewall-cmd --add-service=pop3s 							   |`add item to firewall via service`		   | 
|firewall-cmd --zone=public --add-port=4545/tcp --permanent    |`add item to firewall via port` 		   | 
|firewall-cmd --zone=public --remove-port=4545/tcp --permanent |`remove item from firewall via port`	   |
|firewall-cmd --list-all 									   |`get complete list` 					   |
|firewall-cmd --list-services 								   |`get list of assigned services` 		   |
|firewall-cmd --list-all-zones 								   |`get complete list for all zones`		   |
|firewall-cmd --get-zones 									   |`get list of zones`						   |
|firewall-cmd --get-services 								   |`get list of services` 					   | 
|firewall-cmd --get-default-zone					  		   |`get default zone` 						   |
|firewall-cmd --set-default-zone=work     					   |`set default zone` 						   |
|firewall-cmd --get-active-zones          					   |`get active zones`						   |
|firewall-cmd --get-zone-of-interface=enp0s3 				   |`get zone by interface` 				   |
|firewall-cmd --zone=work --add-interface=enp0s3 			   |`set zone for interface` 				   |	
|firewall-cmd --reload 										   |`make changes permanent if added via port` |
|firewall-cmd --runtime-to-permanent 						   |`change runtime configurtion to permanent` |

> #### Netstat and SS

|Command      |Explanation          	|
|-------------|-------------------------|
|ss -tln 	  |`listening connections` 	|
|ss -tn 	  |`established connections`|
|netstat -tln |`listening connections` 	|
|netstat -tn  |`established connections`|


## User management



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
|apt install openssh-server 				    	   |`install package to be able to connect via shh`|
|apt install xrdp 									   |`install package to be able to connect via rdp`|
|firewall-cmd --add-service=ssh 					   |`enable ssh on firewall` 					   |
|firewall-cmd --permament --zone=public --port=3389/tcp|`enable xrd protocol on firewall` 			   |
|firewall-cmd --reload 								   |`apply firewall changes` 					   |
|ifconfig 											   |`show ip address` 							   |


## Bash programing


## AWK


## SED


## Server management
