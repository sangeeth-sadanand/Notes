# HDFS - Hadoop Distributed File System

- Data node stores the actual data
- Name node stores the metadata, it stores information about the where the chunk of file is to be read from
- Decrease the block size increases scope of parallel processing but the downside is the name node now need to store more meta data.
- Increasing the block size decrease the scope of parallel processing
- Admins can change block size according to the use case.
- We can add more data node if the data size increases.
- In newer version of Hadoop a concept of name node federation where we can split the meta data across multiple name nodes for scalability of name nodes.
- Replication factor is used to replicate the block is n nodes example replication factor is 3 then a block is stored in 3 nodes.
- Secondary name node is used for fault tolerance.
- name node federation is for scalability
- Rack is a set of node that kept in single geographical location
- Admins should not store the all three copies in on single rack.

## How the files are read?

![](media/002_HDFS/09c4d889da0df98be08a9e5649f6c896a12053cf.svg)

## Hadoop Commands

It is similar to [Linux commands](../001_linux/001_commands.md)

- ``hadoop fs`` list all command used in hadoop

- `hdfs dfs` is same as `hadoop fs`

- In most of the command it is communicated with name node. for some command like cat, head it will also communicate with the data node.

- `-appendToFile <localsrc> ... <dst>`: command is used to append data from one or more local files to a file in the Hadoop Distributed File System (HDFS)

- `-cat [-ignoreCrc] <src> ...`: to view the contents 

- `-checksum [-v] <src> ...`: In the context of Hadoop, a **checksum** is a value calculated from a data set and used to verify the integrity of data.

- `-chgrp [-R] GROUP PATH...`/: The `chgrp` command in Linux is used to change the group ownership of files and directories.

- `-chmod [-R] <MODE[,MODE]... | OCTALMODE> PATH...`| change the permission of a file or directory

- `-chown [-R] [OWNER][:[GROUP]] PATH...`: Change the ownership of a file or directory

- `-copyFromLocal [-f] [-p] [-l] [-d] [-t <thread count>] <localsrc> ... <dst>`: copy a file local to HDFS

- `-copyToLocal [-f] [-p] [-ignoreCrc] [-crc] <src> ... <localdst>`: copy file HDFS to local directory

- `-count [-q] [-h] [-v] [-t [<storage type>]] [-u] [-x] [-e] <path> ...`: To count the number of files and directories in a specified path

- `-cp [-f] [-p | -p[topax]] [-d] <src> ... <dst>`: copy file from src to dest in HDFS

- `-createSnapshot <snapshotDir> [<snapshotName>]`:  In Hadoop, creating a snapshot allows you to capture the state of a file system at a specific point in time.

- `-deleteSnapshot <snapshotDir> <snapshotName>`: Delete a snapshot.

- `-df [-h] [<path> ...]`: the `df` (disk free) command is used to check the disk space usage of the HDFS

- `-du [-s] [-h] [-v] [-x] <path> ...`: is used to estimate the space used by files and directories in HDFS

- `-expunge [-immediate] [-fs <path>]`: the `expunge` command is used to permanently remove files and directories from the trash.

- `-find <path> ... <expression> ...`: The `find` command in Hadoop allows you to search for files and directories in HDFS based on various criteria.

- `-get [-f] [-p] [-ignoreCrc] [-crc] <src> ... <localdst>`: copy file HDFS to local directory

- `-getfacl [-R] <path>`: The `getfacl` command in Linux is used to get the Access Control Lists (ACLs) of files and directories.

- `-getfattr [-R] {-n name | -d} [-e en] <path>`: The `getfattr` command in Linux is used to retrieve the extended attributes of files and directories.

- `-getmerge [-nl] [-skip-empty-file] <src> <localdst>`: The `getmerge` command in Hadoop is used to merge multiple files in the Hadoop Distributed File System (HDFS) into a single local file.

- `-head <file>`: Print the head data.

- `-help [cmd ...]`: prints help for the command

- `-ls [-C] [-d] [-h] [-q] [-R] [-t] [-S] [-r] [-u] [-e] [<path> ...]`: list files and directories

![](media/002_HDFS/9576fb1973708f0f9e4686af48ad74226f1e680e.svg)

- `-mkdir [-p] <path> ...`: make directory
- `-moveFromLocal <localsrc> ... <dst>`: move the file from local to HDFS
- `-moveToLocal <src> <localdst>`: move the file from HDFS to local
- `-mv <src> ... <dst>` move file from src to dest within HDFS
- `-put [-f] [-p] [-l] [-d] <localsrc> ... <dst>`: copy file from local directory to HDFS
- `-renameSnapshot <snapshotDir> <oldName> <newName>`: Rename the snapshot
- `-rm [-f] [-r|-R] [-skipTrash] [-safely] <src> ...`: Remove the file 
- `-rmdir [--ignore-fail-on-non-empty] <dir> ...`: remove directory
- `-setfacl [-R] [{-b|-k} {-m|-x <acl_spec>} <path>]|[--set <acl_spec> <path>]`: The `setfacl` command in Linux is used to set Access Control Lists (ACLs) for files and directories.
- `-setfattr {-n name [-v value] | -x name} <path>`: The `setfattr` command in Linux is used to set extended attributes of files and directories.
- `-setrep [-R] [-w] <rep> <path> ...`: The `setrep` is used to change the replication factor of files in the Hadoop Distributed File System (HDFS).
- `-stat [format] <path> ...`: is used to display detailed information about files and directories.
- `-tail [-f] [-s <sleep interval>] <file>`: print tail data.

## HDFS alternative

- AWS - amazon S3 
- Azure - ADLS gene

## Distributed file system vs Object based Storage

### Distributed File System (DFS)

- **Structure**: File-based, organized in a hierarchical directory structure.
- **Access Method**: Typically accessed through file systems interfaces (like HDFS for Hadoop).
- **Data Management**: Handles metadata and data separately, often requiring a master node to manage the file system namespace.
- **Use Cases**: Suited for workloads with a large number of small files and operations that require file-level access (e.g., log storage, Hadoop MapReduce jobs).
- **Consistency**: Ensures strong consistency and often supports transactional updates.
- **Performance**: Designed for high throughput, particularly with sequential reads/writes, but may face challenges with random access patterns.

### Object-Based Storage

- **Structure**: Object-based, data is stored as objects in a flat address space, without hierarchy.
- **Access Method**: Accessed via RESTful APIs (like Amazon S3, Azure Blob Storage).
- **Data Management**: Each object includes metadata, which is managed along with the data, often simplifying scalability and management.
- **Use Cases**: Ideal for unstructured data such as media files, backups, archives, and big data analytics that benefit from massive scalability and easy accessibility.
- **Consistency**: Often provides eventual consistency, though some systems offer strong consistency options.
- **Performance**: Optimized for scalability and managing large volumes of data with excellent redundancy and fault tolerance.

### Key Differences

- **Hierarchy vs. Flat**: DFS uses hierarchical file systems, whereas Object Storage uses a flat structure.
- **APIs vs. File Interfaces**: DFS is accessed via file system interfaces, while Object Storage uses APIs.
- **Metadata Management**: DFS separates metadata from data, while Object Storage combines them in objects.
- **Consistency**: DFS often ensures strong consistency, whereas Object Storage might offer eventual consistency with optional strong consistency.
- **Scalability**: Object Storage generally provides better scalability and fault tolerance for large amounts of unstructured data compared to DFS.
