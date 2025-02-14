---
title: MITRE ATT&CK Framework
author: Jeongwon
date: 2025-01-10 12:29:00 +0900
categories: [Career, PurpleTeam]
tags: [writing]
render_with_liquid: false
---
## MITRE ATT&CK Framework 

###### `REF` : [MITRE](https://attack.mitre.org/) | [IBM](https://www.ibm.com/think/topics/mitre-attack)

---
## About ATT&CK
 ATT&CK(Adversarial Tactics, Techniques & Common Knowledge) Framework는 사이버 범죄자(Cybercriminals)의 알려진 악의적 행동(Known adversarial behaviors)을 기반으로 `사이버 보안 위협을 모델링, 탐지, 예방 및 대응`하기 위해 어디서나 액세스 가능하고 지속적으로 업데이트되는 `지식 기반(Knowledge base)`입니다.

 
---
## ATT&CK Components


### Tactics
Tactics는 공격자가 달성하려는 상위 목표를 나타냅니다. 이는 공격의 단계를 나타내며, 각 단계는 특정 목표를 달성하기 위한 기법과 연결됩니다. Tactics는 공격자의 의도를 이해하고 방어 전략을 수립하는 데 중요한 역할을 합니다.

`TA0001 : Initial Access` : 공격자가 시스템에 처음 접근하는 단계를 의미합니다. 예를 들어, 공격자는 피싱 메일을 통해 피해자의 시스템에 악성 코드를 배포할 수 있습니다.


### Techniques
Tecniques은 Tactics를 달성하기 위해 사용하는 구체적인 방법입니다. 각 Techniques는 공격자가 특정 목표를 달성하기 위해 사용하는 기술적 접근 방식을 설명합니다. Technique는 공격자의 행동을 이해하고 방어 체계를 강화하는 데 중요한 참고 자료입니다.

`T1566 : Phishing` : 공격자가 피해자를 속여 악성 링크나 첨부 파일을 열게 하는 기법입니다. 예를 들어, 공격자는 피해자에게 중요한 문서인 척하며 악성 파일을 첨부한 이메일을 보낼 수 있습니다.


### Sub-Techniques
Sub-Techniques은 Techniques을 더 세부적으로 분류한 것입니다. 이는 공격자의 행동을 더 정확하게 이해하고 방어하기 위해 사용됩니다. Sub-Techniques은 공격자의 구체적인 실행 방법을 파악하는 데 도움을 줍니다.

`T1566.001 : Spear Phishing Attachment` : Phishing의 Sub-Techniques으로, 공격자가 특정 대상에게 악성 파일이 첨부된 이메일을 보내는 것을 의미합니다. 예를 들어, 공격자는 회사의 재무 담당자에게 위조된 세금 문서를 첨부한 이메일을 보낼 수 있습니다.


### Procedures
Procedures는 실제 공격 사례에서 관찰된 구체적인 실행 단계입니다. 이는 공격자의 행동 패턴을 이해하고 방어 전략을 수립하는 데 중요한 참고 자료입니다. Procedures는 공격자가 특정 Tecniques를 어떻게 실행하는지 상세히 설명합니다.

`C0028 : 2015 Ukraine Electric Power Attack` : 2015 Ukraine Electric Power Attack 동안 Sandworm team은 피싱 이메일을 통해 전달된 Microsoft Office 첨부 파일을 사용하여 많은 IT 시스템에 Initial Access를 마련했습니다. 


### Mitigations
Mitigations는 공격자의 Tecniques를 방어하거나 영향을 줄이기 위한 조치입니다. 이는 공격자의 행동을 예방하거나 방어 체계를 강화하는 데 사용됩니다. Mitigations는 조직의 보안 상태를 개선하는 데 중요한 역할을 합니다.

`M1049 : Antivirus/Antimalware` : Antivirus/Antimalware는 의심스러운 파일을 자동으로 격리할 수 있습니다.


### Detection
Detection은 공격자의 행동을 식별하기 위한 방법입니다. 이는 공격자의 Tecniques을 탐지하고 대응하는 데 사용됩니다. Detection는 보안 팀이 공격을 조기에 발견하고 대응할 수 있도록 지원합니다.

`DS0015 : Application Log Content` : Spear Phishing Attachment를 방어하기 위해 DKIM+SPF와 이메일 헤더 분석을 통해 발신자 스푸핑을 탐지하고, Antivirus/Antimalware로 악성 첨부 파일을 스캔하여 차단합니다. 또한, Microsoft Office 등 생산성 소프트웨어에서 의심스러운 하위 프로세스 생성 여부를 모니터링해 악성 코드 실행을 조기에 탐지하고 방어할 수 있습니다.

---

 

 



 

 

 




