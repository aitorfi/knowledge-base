---
layout: default
title: struct stat
parent: sys/stat.h
grand_parent: C Programming Language
---

# struct stat

C
{: .label .label-blue }

Structure
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [stat function](../stat-function)

The `struct stat` structure is used to store information about a file, directory, or symbolic link obtained using functions like `stat`, `fstat`, or `lstat`.

## Members

- **dev_t st_dev:** The device ID of the device containing the file.

- **ino_t st_ino:** The inode number of the file.

- **mode_t st_mode:** The file type and mode (permissions).

- **nlink_t st_nlink:** The number of hard links to the file.

- **uid_t st_uid:** The user ID of the owner of the file.

- **gid_t st_gid:** The group ID of the owner of the file.

- **dev_t st_rdev:** The device ID (if the file is a special file).

- **off_t st_size:** The size of the file in bytes.

- **blksize_t st_blksize:** The optimal block size for file I/O.

- **blkcnt_t st_blocks:** The number of blocks allocated for the file.

- **struct timespec st_atim:** The time of last access.

- **struct timespec st_mtim:** The time of last modification.

- **struct timespec st_ctim:** The time of last status change.

## Usage example

```c
#include <stdlib.h>
#include <stdio.h>
#include <sys/stat.h>

int main(void)
{
    const char *file_path = "example.txt";
    struct stat file_info;

    if (stat(file_path, &file_info) == -1)
    {
        perror("Failes to retrieve file information");
        return (EXIT_FAILURE);
    }
    printf("File size: %lld bytes\n", (long long)file_info.st_size);
    printf("File permissions: %o\n", file_info.st_mode & 0777);
    printf("Number of hard links: %ld\n", (long)file_info.st_nlink);
    return (EXIT_SUCCESS);
}
```
