# Linux Directory structure
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
https://explainshell.com/
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

## Directories

> #### Symbols explonations

|Symbol                 |Explanation                    |
|-----------------------|-------------------------------|
|.                      |`This directory`               |
|\.\.                   |`Parent directory`             |
|/                      |`Root`                         |
|~                      |`Home`					        |

> #### Commands for manipulation

|Command                 |Explanation                   |
|-----------------------|-------------------------------|
|cd /home/ecneb         |`Change directory`             |
|mkdir test             |`Create directory`             |
|mkdir -p t1/t2/t3      |`Create directory recursively` |
|rmdir test             |`Remove directory`				|
|rmdir -p t1/t2/t3      |`Remove directory recursively` |
|ls  					|`Show directory contents`      |
|ls -l      			|`Show in list format`          |
|ls -a      			|`Show hidden files`            |
|ls -t     				|`Sort by time`                 |
|ls -h      			|`Human readable file size`     |
|ls -r      			|`Reverse order`                |
|ls -Z      			|`Show SELinux context`         |
|tree   				|`Show contents in graph format`|
|tree -d      			|`Show only directories`        |

## Permissions
> #### Example

|Type|User permissions|Group permissions|Other permissions|Number of elments|    Owner|    Creator|   Size|    Date creation|    Time creation|   Name|
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

|Keys				 |Explanation 							             |
|--------------------|---------------------------------------------------|
|^G    (F1)      	 |Display this help text							 |
|^X    (F2)      	 |Close the current file buffer / Exit from nano	 |
|^O    (F3)    		 |Write the current file to disk					 |
|^R    (F5)      	 |Insert another file into the current one			 |
|^W    (F6)      	 |Search forward for a string or a regular expression|
|^\    (M-R)     	 |Replace a string or a regular expression			 |
|^K    (F9)       	 |Cut the current line and store it in the cutbuffer |
|^U    (F10)     	 |Uncut from the cutbuffer into the current line	 |
|^J    (F4)      	 |Justify the current paragraph						 |  
|^T    (F12)   		 |Invoke the spell checker, if available			 |
|^C    (F11)    	 |Display the position of the cursor				 |
|^_    (M-G)    	 |Go to line and column number						 |
|M-U           		 |Undo the last operation							 |
|M-E            	 |Redo the last undone operation					 |
|M-A   (^6)      	 |Mark text starting from the cursor position		 |
|M-6   (M-^)     	 |Copy the current line and store it in the cutbuffer|
|M-]             	 |Go to the matching bracket						 |
|M-W   (F16)     	 |Repeat the last search							 |
|M-▲             	 |Search next occurrence backward					 |
|M-▼             	 |Search next occurrence forward					 |
|^B    (◀)       	 |Go back one character								 |
|^F    (▶)       	 |Go forward one character							 |
|^◀    (M-Space) 	 |Go back one word									 |
|^▶    (^Space)  	 |Go forward one word								 |
|^A    (Home)    	 |Go to beginning of current line					 |
|^E    (End)     	 |Go to end of current line							 |
|^R + ^X    		 |Execute command									 |	
|^R + ^T    		 |To file											 |
|^R + M-F    		 |New Buffer										 |
|M-, 				 |Next Buffer										 |
|M-, 				 |Previous Buffer									 |
|M-Shift A 			 |Select mounted									 |
|M-Shift 6 			 |Copy												 |
|^U  				 |Pase												 |
	
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

|Command       																  |Explanation                      |
|-----------------------------------------------------------------------------|---------------------------------|
|ssh ecneb@127.0.0.1 														  |`Connect via ssh` 			    |
|exit 				 														  |`Exit from ssh` 					|
|scp ecneb@127.0.0.1:/home/ecneb/Downloads/test/docker-compose.yml /home/ecneb|`Copy from server to local PC` 	|
|scp /home/ecneb/Desktop/test.zip ecneb@127.0.0.1:/home/ecneb/Downloads  	  |`Copy from local PC to server`	|
|sftp ecneb@127.0.0.1 													      |`Connect via sftp` 				|
|bye 																		  |`Exit from sftp` 				|
|get 																		  |`Download file` 					|
|put 																		  |`Upload file` 					|
|rm 																		  |`Remove file` 					|



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

