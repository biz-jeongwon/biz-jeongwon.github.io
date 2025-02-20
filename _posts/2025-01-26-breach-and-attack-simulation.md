---
title: Breach and Attack Simulation
author: Jeongwon
date: 2025-02-15 13:19:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## BAS (Breach and Attack Simulation)

###### `REF` : [Caldera git](https://github.com/mitre/caldera)

`BAS(Breach and Attack Simulation)`는 조직의 보안 상태를 평가하기 위해 실제 공격 시나리오를 시뮬레이
션하는 기술입니다. 이를 통해 조직의 방어 체계가 실제 공격에 얼마나 효과적으로 대응할 수 있는지 테스트하고, 취약점을 식별하여 개선할 수 있습니다.

---
## Caldera
`Caldera`는 MITRE Corporation에서 개발한 오픈소스 자동화된 침해 시뮬레이션 플랫폼으로, 조직의 보안 방어 체계를 테스트하고 개선하기 위해 설계되었습니다. `Caldera`는 MITRE ATT&CK 프레임워크를 기반으로 하여 실제 공격자의 전술, 기술, 절차(TTPs)를 시뮬레이션함으로써 조직의 보안 취약점을 식별하고 대응 능력을 평가합니다.

---
## To use Caldera (in local WSL2)

##### Environment Seeings
```bash
sudo apt update
sudo apt install git python3-pip
```

##### Caldera Install
```bash
git clone https://github.com/mitre/caldera.git --recursive
cd caldera

python3 -m venv caldera-venv
source caldera-venv/bin/activate
pip install -r requirements.txt
python3 server.py --insecure
```

##### ++ Trouble Shooting
```bash
git submodule init
npm install
npm run build
```

---
## To use Caldera (in remote AWS)

##### Environment Seeings
```bash
ssh -i /path/to/your-key.pem ubuntu@your-instance-public-ip
sudo su -
sudo apt-get update
sudo apt-get install -y git python3-pip
```

##### Caldera Install
```bash
git clone https://github.com/mitre/caldera.git --recursive
cd caldera

python3 -m venv caldera-venv
source caldera-venv/bin/activate
pip install -r requirements.txt
python3 server.py --insecure --build
```

##### ++ Trouble Shooting
```bash
## 의존성
sudo apt install golang-go npm
pip install docker
pip install setuptools

git submodule init
cd ~/caldera/plugins/magma # caldera 경로
npm install
npm run build

## AWS 공간 확보 (Storage 늘려놓는게 나음)
sudo swapoff -v /swapfile
sudo rm /swapfile
sudo fallocate -l 8G /swapfile  # 8GB로 변경
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf

sudo sysctl -p
node --max-old-space-size=4096 app.js

```





