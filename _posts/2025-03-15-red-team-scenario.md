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

초기 침투 → 정보 수집 <br>
→ 권한 상승 → 횡적 이동 → 권한 상승 → 횡적 이동 ... <br>
→ 목표 달성 <br>

### Configure Scenario with Caldera
Caldera는 기본적으로 초기 침투된 환경을 가정하므로, 이는 제외하였습니다.

#### 정보 수집
Target과 관련된 정보를 수집하는 단계. hostname, OS version, pslist, mitigation 등등 호스트 정보를 수집하여 대상 호스트에서 권한 상승을 진행할 지, 다른 호스트로 횡적 이동을 수행할 지 등을 판단합니다.
(Bloodhount 툴을 활용하거나, SMB 쉐어에서 정보 수집을 수행할 수 있습니다.)

#### 권한 상승

#### 횡적 이동





