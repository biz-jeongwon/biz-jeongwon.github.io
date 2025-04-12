---
title: Red-Team Framework - (2) Caldera with Sliver, Metasploit
author: Jeongwon
date: 2025-04-07 23:15:00 +0900
categories: [Career, RedTeam]
tags: [writing]
render_with_liquid: false
---
## Environment
(AWS t3.xlarge)<br><br>

### Caldera

#### Install Caldera
```bash
sudo apt-get update
sudo apt-get install -y git python3-pip python3.12-venv golang-go npm
git clone https://github.com/mitre/caldera.git --recursive
cd caldera
python3 -m venv caldera-venv

source caldera-venv/bin/activate
pip install -r requirements.txt
pip install docker
pip install setuptools
python3 server.py --insecure --build
```

#### Configure Daemon
```bash
vi /etc/systemd/system/caldera.service

#  [Unit]
#  Description=Caldera Server
#  After=network.target

#  [Service]
#  Type=simple
#  User=root
#  WorkingDirectory=/root/PARASITE/caldera
#  ExecStart=/bin/bash -c 'source /root/PARASITE/caldera/caldera-venv/bin/activate && #  exec python3 /root/PARASITE/caldera/server.py --insecure --build'
#  Restart=always

#  [Install]
#  WantedBy=multi-user.target

sudo chmod 644 /etc/systemd/system/caldera.service
sudo systemctl daemon-reexec
sudo systemctl daemon-reload

sudo systemctl enable caldera.service
sudo systemctl start caldera.service

sudo systemctl status caldera.service
```
<br><br>

### Sliver

#### Install Sliver
```bash
sudo apt update
sudo apt install -y git golang make zip

echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc

git clone https://github.com/BishopFox/sliver.git
cd sliver

make
```

#### Configure Daemon
```bash
vi /etc/systemd/system/sliver.service

#  [Unit]
#  Description=Sliver C2 Server
#  After=network.target

#  [Service]
#  Type=simple
#  User=root
#  WorkingDirectory=/root/PARASITE/sliver
#  ExecStart=/root/PARASITE/sliver/sliver-server
#  Restart=always

#  [Install]
#  WantedBy=multi-user.target

sudo chmod 644 /etc/systemd/system/sliver.service
sudo systemctl daemon-reexec
sudo systemctl daemon-reload

sudo systemctl enable sliver.service
sudo systemctl start sliver.service

sudo cp ./sliver-server /usr/local/bin/sliver-server
sudo cp ./sliver-client /usr/local/bin/sliver-client
```
<br><br>

### Sliver

```bash
python3 -m venv sliver-env
source sliver-env/bin/activate
pip install grpcio grpcio-tools

python3 -m grpc_tools.protoc \
  -I=protobuf \
  --python_out=. \
  --grpc_python_out=. \
  protobuf/sliverpb/sliver.proto \
  protobuf/rpcpb/services.proto \
  protobuf/commonpb/common.proto

mkdir -p ~/caldera/plugins/sliver_plugin/sliver_grpc
cp sliverpb/*_pb2*.py rpcpb/*_pb2*.py commonpb/*_pb2*.py ~/caldera/plugins/sliver_plugin/sliver_grpc/
```
