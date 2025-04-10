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
<br><br>

### Sliver
```bash
sudo apt update
curl https://sliver.sh/install|sudo bash
systemctl start sliver
sliver
```

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
