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
## ATT&CK Features

### 플랫폼(Enterprise, Mobile, ICS) 별 구분
-  Enterprise : 가장 일반적으로 공격 대상이 되는 환경입니다. Windows, Linux, MacOS, Cloud 환경이 그 예시입니다.
    - Windows
      - T1059.001: Command and Scripting Interpreter (PowerShell)
      - T1112: Modify Registry
      - T1055: Process Injection (DLL Injection)
      - T1546.003: Event Triggered Execution (Windows Management Instrumentation)
    - Linux
      - T1059.004: Command and Scripting Interpreter (Unix Shell)
      - T1053.003: Scheduled Task/Job (Cron)
      - T1548.001: Abuse Elevation Control Mechanism (Setuid and Setgid)
      - T1064: Scripting
    - MacOS
      - T1546.004: Event Triggered Execution (Launch Agent)
      - T1553.002: Subvert Trust Controls (Gatekeeper Bypass)
      - T1547.011: Boot or Logon Autostart Execution (Plist Modification)
      - T1059.004: Command and Scripting Interpreter (Unix Shell)
    - Cloud
      - T1538: Cloud Service Discovery
      - T1552.002: Unsecured Credentials (Cloud Instance Metadata API)
      - T1078.004: Valid Accounts (Azure AD)
      - T1611: Escape to Host (Kubernetes Exploitation)
    
  - Mobile : 모바일 기기는 개인 및 기업 데이터에 접근할 수 있는 주요 매개체로, 공격 대상이 되고 있습니다. Android는 오픈 소스 기반으로 취약점이 더 자주 발견되며, iOS는 폐쇄적 생태계로 상대적으로 안전하지만 제로데이 공격에 취약합니다.
    - Android
      - T1404: Exploit Public-Facing Application (Malicious App Installation)
      - T1620: Abuse Elevation Control Mechanism (Rooting)
      - T1433: Access Location Data
      - T1430: Exploitation for Privilege Escalation
    - iOS
      - T1406: Exploit Public-Facing Application (Jailbreaking)
      - T1553.003: Subvert Trust Controls (Code Signing Bypass)
      - T1546.004: Event Triggered Execution (Launch Agent)
      - T1430: Exploitation for Privilege Escalation

  - ICS : ICS와 OT(Operational Technology) 환경은 물리적 프로세스를 제어하는 시스템으로, 공격 시 물리적 피해가 발생할 수 있습니다. 이 환경은 실시간 운영이 중요하며, 패치가 어렵고 오래된 시스템이 많아 취약합니다.
    - T0889: Manipulation of Control (PLC Manipulation)
    - T0859: Exploitation of Remote Services (SCADA Exploitation)
    - T0866: Protocol Manipulation (Modbus/DNP3 Spoofing)
    - T0883: Denial of Service (Physical Process Disruption)
    
### 실용성
- 공격 탐지: 공격자의 행동 패턴을 기반으로 탐지 규칙을 개발.
- 방어 전략 수립: 조직의 방어 체계를 강화하기 위한 전략 수립.
- 레드팀/블루팀 훈련: 공격 시뮬레이션을 통해 팀의 역량 강화.
- 보안 솔루션 평가: MITRE의 공격 시뮬레이션(Evaluations)을 통해 보안 제품의 성능 검증.

### 동적 업데이트
실제 공격 사례를 기반으로 새로운 기법과 절차가 추가됩니다. 그리고 신흥 기술(클라우드, SaaS)과 최신 공격 기법을 반영하여 지속적으로 업데이트됩니다.

---
## Differences
VS Cyber Kill Chain : 공격의 단계를 선형적으로 설명하는 것에 반해 MITRE ATT&CK은 공격의 단계별 구체적 기법을 강조하였습니다.

VS Diamond Model: 공격의 4가지 요소(공격자, 인프라, 능력, 피해자)를 강조한 것에 반해 MITRE ATT&CK은 공격자의 실행 방법에 초점을 맞추었습니다.

 

 



 

 

 




