---
title: Elevation of privilege with caldera
author: Jeongwon
date: 2025-03-15 22:08:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## Elevation of privilege

### SUID Binary Poisoning

###### SUID Binary
SUID(Set User ID) Binary는 특정 실행 파일이 파일 소유자의 권한으로 실행되도록 설정된 파일입니다. 이는 일반 사용자가 실행해도, 해당 Binary가 소유자의 권한으로 실행된다는 의미입니다.
<br>
![image](assets/img/elevation-of-privilege-with-caldera/suid_binary.png)
예시로 passwd가 있습니다. 이는 파일 소유자가 root이지만, `-rwsr-xr-x`에서와 같이 SUID가 활성화되어있기 때문에 일반 사용자가 실행해도 파일 소유자인 root의 권한으로 실행할 수 있습니다.
