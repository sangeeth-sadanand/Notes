# Linux commands

- Linux follows tree structure
- `~` represents home directory of the users.
- `..` represent parent directory
- `.` represent current directory

## Permission structure

![](media/001_commands/b610e0bad3f4ce30dd179cf9fcc889e0fba38a15.svg)

r - read (4)
w - write(2)
x - execute(1)

| command                                        | description                                                                                     |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| pwd                                            | prints present corking directory                                                                |
| whoami                                         | print current username                                                                          |
| clear                                          | clears terminal screen                                                                          |
| cd                                             | change directory                                                                                |
| cd -                                           | change to previous directory                                                                    |
| cd ~                                           | change to home                                                                                  |
| cd ..                                          | go one directory up                                                                             |
| ls                                             | list directory content <br>**blue** color indicates directory<br>**green** indicates executable |
| ls -l                                          | long list                                                                                       |
| ls -lt                                         | list content with long list order with latest modified date                                     |
| Is -Itr                                        | list content with long list order with oldest file first                                        |
| Is -IR                                         | Recursively list all the files in a directory                                                   |
| Is -a                                          | list all files including hidden files                                                           |
| touch                                          | To create an empty file                                                                         |
| chmod \<permissions\> \<file_name\>            | To change file permissions                                                                      |
| cat \<file_name\>                              | see the content of file                                                                         |
| mkdir \<file_name\>                            | make a new directory                                                                            |
| rmdir \<directory\>                            | removes an empty directory                                                                      |
| rm < filename >                                | removes the files                                                                               |
| rm -R \<directory\>                            | delete directory even if it is not empty                                                        |
| cp \<source\> \<destination\>                  | Moves the file from source to destination or renames a file                                     |
| cp -R \<source directory\> \<destination_dir\> | Copies source dir to destination dir.                                                           |
| mv \<source\> \<destination\>                  | Moves the file from source to destination or renames a file                                     |
| head \<file_name\>                             | prints 10 lines of the file                                                                     |
| tail \<file_name\>                             | print last 10 lines of the file                                                                 |
| history                                        | see of the past command                                                                         |
| wc                                             | get word count                                                                                  |
| du \<directory\>                               | gives the disk usage of the files & directory                                                   |
| du -h                                          | For memory in human readable format                                                             |
| grep \<search-strings\> \<files\>              | find search-strings in this files                                                               |
