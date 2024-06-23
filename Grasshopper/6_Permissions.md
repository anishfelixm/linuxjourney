## File Permissions

Files have different permissions and file modes. One can see the file permission by doing a simple "**ls -l**". The "ls -l" command will usually have the following output : 

> drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .

The first block in the above output shows the file permissions. The file permissions ie "drwxr-xr-x" can be divided into 4 blocks ie
| d | rwx | r-x | r-x |
The first bit shows type of file. "d" represents a directory while a regular file will have "-". The next 3 blocks represent User permissions, group permissions and other permissions. These 3 blocks represent the actual file permissions.

|charachters|permission|
|---|---|
|r|Read|
|w|Write|
|x|Executable|
|-|Empty|

So in above example we can say user pete has:
