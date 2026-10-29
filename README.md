# Linux-IPC-Shared-memory
Ex06-Linux IPC-Shared-memory

# AIM:
To Write a C program that illustrates two processes communicating using shared memory.

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - Shared Memory

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## Write a C program that illustrates two processes communicating using shared memory.
~~~
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main(void)
{
    key_t key = ftok(".", 65);

    if (key == -1) {
        perror("ftok");
        return 1;
    }

    int shmid = shmget(key, 1024, 0666 | IPC_CREAT);

    if (shmid == -1) {
        perror("shmget");
        return 1;
    }

    printf("Shared memory id = %d\n", shmid);

    char *str = (char *)shmat(shmid, NULL, 0);

    if (str == (char *)-1) {
        perror("shmat");
        return 1;
    }

    printf("Write Data : ");
    if (fgets(str, 1024, stdin) == NULL) {
        shmdt(str);
        return 1;
    }

    printf("Data written in memory: %s", str);

    shmdt(str);

    return 0;
}
~~~




## OUTPUT
<img width="722" height="566" alt="image" src="https://github.com/user-attachments/assets/fccdf573-1489-4e08-b414-a361095b43d3" />


# RESULT:
The program is executed successfully.
