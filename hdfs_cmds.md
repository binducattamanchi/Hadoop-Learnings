* `hadoop version`
* `hadoop fs –mkdir /path/directory_name`
* `hadoop fs -ls /path`
* `hadoop fs -put <localsrc> <dest>`
* `hadoop fs -copyFromLocal <localsrc> <hdfs destination>``
* `hadoop fs -get <src> <localdest>`
* `hadoop fs -copyToLocal <hdfs source> <localdst>`
* `hadoop fs –cat /path_to_file_in_hdfs`
* `hadoop fs -mv <src> <dest>`
* `hadoop fs -cp <src> <dest>`
* `hadoop fs -moveFromLocal <localsrc> <dest>`
* `hadoop fs -tail [-f] <file>`
* `hadoop fs -rm /path/file.txt`
* `hadoop fs -expunge  //this is to clear trash`
* `hadoop fs -chown [-R] [owner] [:[group]] <path>. //change owner`
* `hadoop fs -chgrp <group> <path>`
* `hadoop fs -setrep <rep> <path>. //set replication factor`
* `hadoop fs -du –s /directory/filename //disk usage check`
* `hadoop fs -df [-h] <path> //shows capacity, size and usage`
* `hadoop fsck <path> [ -move | -delete | -openforwrite] [-files [-blocks [-locations | -racks]]] //checks health of hdfs`
* `hadoop fs –touchz /directory/filename`
* `hadoop fs -test  -[defsz] <path> //file test operations`
  ```
  Options	Description
  * `-d	Check whether the path given by the user is a directory or not, return 0 if it is a directory.`
  * `-e	Check whether the path given by the user exists or not, return 0 if the path exists.`
  * `-f	Check whether the path given by the user is a file or not, return 0 if it is a file.` 
  * `-s	Check if the path is not empty, return 0 if a path is not empty.`
  * `-r	return 0 if the path exists and read permission is granted`
  * `-w	return 0 if the path exists and write permission is granted`
  * `-z	Checks whether the file size is 0 byte or not, return 0 if the file is of 0 bytes.`
  ```

* `hadoop fs -text <src> //converts and show data in text format`
* `hadoop fs -stat [format] <path> //provides file stats`
  ```
   Formats:
   %b –    file size in bytes
   %g –    group name of owner
   %n –    file name
   %o –    block size
   %r  –    replication
   %u –    user name of owner
   %y –    modification date
   ```
   
* `hadoop fs -usage <command> //shows the required command details like syntax`
* `hadoop fs -help [command] //like man page`
* `hadoop fs -chmod [-R] <mode> <path>`
* `hadoop fs -appendToFile <localsrc> <dest>`
* `hadoop fs -checksum <src> `
* `hadoop fs -count [options] <path>`
  ```
  -q  –  shows quotas(quota is the hard limit on the number of names and amount of space used for individual directories)
  -u  –  it limits output to show quotas and usage only
  -h  –  shows sizes in a human-readable format
  -v  –  shows header line
  ```
* `hadoop fs -find <path> … <expression>`
* `hadoop fs -getmerge <src> <localdest>`
