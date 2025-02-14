---
title: MITRE ATT&CK Framework
author: Jeongwon
date: 2025-01-10 12:29:00 +0900
categories: [Career, PurpleTeam]
tags: [writing]
render_with_liquid: false
---
### MITRE ATT&CK Framework 

###### `REF` : [MITRE](https://attack.mitre.org/) | [IBM](https://www.ibm.com/think/topics/mitre-attack)

---
#### About ATT&CK
 ATT&CK(Adversarial Tactics, Techniques & Common Knowledge) Framework는 사이버 범죄자(Cybercriminals)의 알려진 악의적 행동(Known adversarial behaviors)을 기반으로 `사이버 보안 위협을 모델링, 탐지, 예방 및 대응`하기 위해 어디서나 액세스 가능하고 지속적으로 업데이트되는 `지식 기반(Knowledge base)`입니다.

 
---
#### ATT&CK Components


##### Tactics
Tactics는 공격자가 달성하려는 상위 목표를 나타냅니다. 이는 공격의 단계를 나타내며, 각 단계는 특정 목표를 달성하기 위한 기법과 연결됩니다. Tactics는 공격자의 의도를 이해하고 방어 전략을 수립하는 데 중요한 역할을 합니다.

예시) Initial Access : 공격자가 시스템에 처음 접근하는 단계를 의미합니다. 예를 들어, 공격자는 피싱 메일을 통해 피해자의 시스템에 악성 코드를 배포할 수 있습니다.


##### Techniques
Tecniques은 Tactics를 달성하기 위해 사용하는 구체적인 방법입니다. 각 Techniques는 공격자가 특정 목표를 달성하기 위해 사용하는 기술적 접근 방식을 설명합니다. Technique는 공격자의 행동을 이해하고 방어 체계를 강화하는 데 중요한 참고 자료입니다.

예시) Phishing : 공격자가 피해자를 속여 악성 링크나 첨부 파일을 열게 하는 기법입니다. 예를 들어, 공격자는 피해자에게 중요한 문서인 척하며 악성 파일을 첨부한 이메일을 보낼 수 있습니다.


##### Sub-Techniques
Sub-Techniques은 Techniques을 더 세부적으로 분류한 것입니다. 이는 공격자의 행동을 더 정확하게 이해하고 방어하기 위해 사용됩니다. Sub-Techniques은 공격자의 구체적인 실행 방법을 파악하는 데 도움을 줍니다.

예시) Spear Phishing Attachment : Phishing의 Sub-Techniques으로, 공격자가 특정 대상에게 악성 파일이 첨부된 이메일을 보내는 것을 의미합니다. 예를 들어, 공격자는 회사의 재무 담당자에게 위조된 세금 문서를 첨부한 이메일을 보낼 수 있습니다.


##### Procedures
Procedures는 실제 공격 사례에서 관찰된 구체적인 실행 단계입니다. 이는 공격자의 행동 패턴을 이해하고 방어 전략을 수립하는 데 중요한 참고 자료입니다. Procedures는 공격자가 특정 Tecniques를 어떻게 실행하는지 상세히 설명합니다.

예시) 공격자가 레지스트리를 수정하여 악성 코드를 지속적으로 실행하는 절차를 예로 들 수 있습니다. 예를 들어, 공격자는 Windows 레지스트리의 실행 키를 수정하여 시스템이 부팅될 때마다 악성 코드가 실행되도록 설정할 수 있습니다.


##### Mitigations
Mitigations는 공격자의 Tecniques를 방어하거나 영향을 줄이기 위한 조치입니다. 이는 공격자의 행동을 예방하거나 방어 체계를 강화하는 데 사용됩니다. Mitigations는 조직의 보안 상태를 개선하는 데 중요한 역할을 합니다.

예시) 피싱 공격을 방어하기 위해 직원들에게 보안 교육을 실시하는 것은 완화 조치의 예입니다. 예를 들어, 조직은 직원들에게 의심스러운 이메일을 열지 않도록 교육하고, 이메일 필터링 솔루션을 도입하여 악성 메일을 차단할 수 있습니다.


##### Detection
Detection은 공격자의 행동을 식별하기 위한 방법입니다. 이는 공격자의 Tecniques을 탐지하고 대응하는 데 사용됩니다. Detection는 보안 팀이 공격을 조기에 발견하고 대응할 수 있도록 지원합니다.

예시) 레지스트리 수정을 탐지하기 위해 시스템 로그를 모니터링하는 것은 탐지 방법의 예입니다. 예를 들어, 보안 팀은 Windows 레지스트리의 변경 사항을 감시하고, 의심스러운 변경이 발생할 경우 경고를 발생시킬 수 있습니다.

---

 

 



 

 

 




