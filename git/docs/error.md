### (1)
```bash
$ git pull one main
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (17/17), done.
remote: Compressing objects: 100% (16/16), done.
remote: Total 18 (delta 0), reused 17 (delta 0), pack-reused 1
Unpacking objects: 100% (18/18), 4.44 KiB | 66.00 KiB/s, done.
From https://github.com/lmliheng/codes
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> one/main
fatal: refusing to merge unrelated histories
```
### (2)
```bash
$ git pull one master
fatal: unable to access 'https://github.com/lmliheng/codes.git/': OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 0
```
### (3)
```bash
$ git pull one main
fatal: unable to access 'https://github.com/lmliheng/codes.git/': Failed to connect to github.com port 443 after 21104 ms: Couldn't connect to server
```