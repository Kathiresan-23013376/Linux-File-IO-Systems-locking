# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 

```
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h> // Include for debugging

int main() {
    char block[1024];
    int in, out;
    int nread;

    // Open input file
    in = open("filecopy.c", O_RDONLY);
    if (in == -1) {
        perror("Error opening input file");
        exit(1);
    }
    printf("Input file opened successfully\n");

    // Open or create output file
    out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
    if (out == -1) {
        perror("Error opening/creating output file");
        exit(1);
    }
    printf("Output file opened/created successfully\n");

    // Read from input file and write to output file
    while ((nread = read(in, block, sizeof(block))) > 0) {
        printf("Read %d bytes from input file\n", nread);
        if (write(out, block, nread) != nread) {
            perror("Error writing to output file");
            exit(1);
        }
        printf("Wrote %d bytes to output file\n", nread);
    }

    if (nread == -1) {
        perror("Error reading from input file");
        exit(1);
    }

    printf("End of input file\n");

    // Close files
    close(in);
    close(out);

    printf("Files closed successfully\n");

    exit(0);
}

```





## 2.To Write a C program that illustrates files locking
```
//C program that illustrates files locking goes here
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>
int main (int argc, char* argv[])
{ char* file = argv[1];
int fd;
struct flock lock;
printf ("opening %s\n", file);
/* Open a file descriptor to the file. */
fd = open (file, O_WRONLY);
// acquire shared lock
if (flock(fd, LOCK_SH) == -1) {
printf("error");
}else
{printf("Acquiring shared lock using flock");
}
getchar();
// non-atomically upgrade to exclusive lock
// do it in non-blocking mode, i.e. fail if can't upgrade immediately
if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
printf("error");
}else
{printf("Acquiring exclusive lock using flock");}
getchar();
// release lock
// lock is also released automatically when close() is called or process exits
if (flock(fd, LOCK_UN) == -1) {
printf("error");
}else{
printf("unlocking");
}
getchar();
close (fd);
return 0;
}

```



## OUTPUT

## FILECOPYING
![Screenshot from 2024-05-07 13-18-53](https://github.com/Kathiresan-23013376/Linux-File-IO-Systems-locking/assets/150008375/0a9d7503-8083-4711-b544-10a764333e47)
![Screenshot from 2024-05-07 13-22-21](https://github.com/Kathiresan-23013376/Linux-File-IO-Systems-locking/assets/150008375/b43e1a1b-98bc-48cb-8148-6fae93945bac)

![Screenshot from 2024-05-07 13-23-08](https://github.com/Kathiresan-23013376/Linux-File-IO-Systems-locking/assets/150008375/561e41a2-8811-4143-9fcc-a37f5c101e0c)


## FILE LOCKING

![Screenshot from 2024-05-07 13-27-18](https://github.com/Kathiresan-23013376/Linux-File-IO-Systems-locking/assets/150008375/0b4969cd-ee4b-49be-af3e-961095f01284)



# RESULT:
The programs are executed successfully.
