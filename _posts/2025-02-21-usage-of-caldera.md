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
Victim host에게 공격 전술을 수행할 수 있는 Agent를 생성하고 관리합니다.

### Campaigns/Abilities
Agent가 Victim host에게 수행할 수 있는 공격 전술입니다.

### Campaigns/Adversaries
`Abilities`의 공격 전술을 Chaining할 수 있습니다.

### Campaigns/Operation
`Adversaries`의 Attack Chain을 실행합니다.

---
## Agents
- `Deploy an agent` 버튼을 클릭하여 Agent를 생성할 수 있습니다.
  ※ Caldera 서버와 동일한 호스트에서 Agent를 생성하려면 `app.contact.http` 자리에 0.0.0.0 대신 localhost를 넣어주면 됩니다.
- Agent의 OS에 맞는 Platform을 선택하고, 제일 위에 존재하는 명령어를 Agent 호스트의 터미널에 입력


