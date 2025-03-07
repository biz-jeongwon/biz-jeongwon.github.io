---
title: Usage of Caldera
author: Jeongwon
date: 2025-02-21 16:04:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## Caldera

###### `REF` : [DOCS](https://caldera.readthedocs.io/en/latest/) | [YOUTUBE](https://www.youtube.com/playlist?list=PLF2bj1pw7-ZvLTjIwSaTXNLN2D2yx-wXH) | [BLOG](https://medium.com/@mitrecaldera/welcome-to-the-official-mitre-caldera-blog-page-f34c2cdfef09) | [WEB](https://caldera.mitre.org/)

---
## Overview

### Campaigns/Agents
Victim host를 생성하고 관리합니다.

### Campaigns/Abilities
Caldera Server가 Victim host에게 수행할 수 있는 공격 전술입니다.

### Campaigns/Adversaries
`Abilities`의 공격 전술을 Chaining할 수 있습니다.

### Campaigns/Operation
`Adversaries`의 Attack Chain을 Victim host에게 실행합니다.

---
## Attack Test

![image](assets/img/usage-of-caldera/agent_create.png)
- `Campaigns/Agents`에서 Victim host를 생성합니다.
    - 저는 Sandcat을 사용하였고, Linux 환경의 Victim host를 택하였습니다.
    - `app.contact.http`의 IP 자리에 Caldera server의 IP를 넣어줍니다.
    - 입력을 마친 후 하단 명령어를 Victim host의 Terminal에서 실행해줍니다.

![image](assets/img/usage-of-caldera/operation_exec.png)
- `Campaigns/Operation`에서 실행할 Attack Chain을 `Campaigns/Adversaries`에서 선택합니다.
    - 예시로 생성되어있던 `Thief`를 실행해 보았습니다.
 




