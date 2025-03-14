---
title: EDR with Wazuh, Sysmon, Sigma
author: Jeongwon
date: 2025-03-08 17:09:00 +0900
categories: [Career, BlueTeam]
tags: [writing]
render_with_liquid: false
---
## Configure EDR with Wazuh, Sysmon, Sigma

### Build Wazuh (with AWS)

##### Install wazuh-indexer
###### `REF` : [Wazuh-indexer Install Guide](https://documentation.wazuh.com/current/installation-guide/wazuh-indexer/step-by-step.html)

```bash
curl -sO https://packages.wazuh.com/4.11/wazuh-certs-tool.sh
curl -sO https://packages.wazuh.com/4.11/config.yml
# config.yml의 IP 자리에 127.0.0.1을 넣어야 합니다. 
```

```bash
bash ./wazuh-certs-tool.sh -A
tar -cvf ./wazuh-certificates.tar -C ./wazuh-certificates/ .
rm -rf ./wazuh-certificates
```

```bash
apt-get install gnupg apt-transport-https
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
apt-get update
# 본 과정은 wazuh-indexer, server, dashboard 모두 수행되어야 한다고 Guide에 나와있지만,
# 한 번만 수행해도 괜찮습니다.
```

```bash
NODE_NAME=node-1
tar -xf ./wazuh-certificates.tar -C /etc/wazuh-indexer/certs/ ./$NODE_NAME.pem ./$NODE_NAME-key.pem ./admin.pem ./admin-key.pem ./root-ca.pem
mv -n /etc/wazuh-indexer/certs/$NODE_NAME.pem /etc/wazuh-indexer/certs/indexer.pem
mv -n /etc/wazuh-indexer/certs/$NODE_NAME-key.pem /etc/wazuh-indexer/certs/indexer-key.pem
chmod 500 /etc/wazuh-indexer/certs
chmod 400 /etc/wazuh-indexer/certs/*
chown -R wazuh-indexer:wazuh-indexer /etc/wazuh-indexer/certs
```

```bash
systemctl daemon-reload
systemctl enable wazuh-indexer
systemctl start wazuh-indexer
```

###### ++ Trouble Shooting

```bash
sudo vi /etc/wazuh-indexer/jvm.options
# 아래 내용 변경
# -Xms512m
# -Xmx512m

sudo apt update
sudo apt install openjdk-17-jre -y

sudo fallocate -l 8G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

<br><br>

##### Install wazuh-server
###### `REF` : [Wazuh-server Install Guide](https://documentation.wazuh.com/current/installation-guide/wazuh-server/step-by-step.html)

```bash
apt-get -y install wazuh-manager
apt-get -y install filebeat
```

```bash
curl -so /etc/filebeat/filebeat.yml https://packages.wazuh.com/4.11/tpl/wazuh/filebeat/filebeat.yml
filebeat keystore create
echo admin | filebeat keystore add username --stdin --force
echo admin | filebeat keystore add password --stdin --force
curl -so /etc/filebeat/wazuh-template.json https://raw.githubusercontent.com/wazuh/wazuh/v4.11.0/extensions/elasticsearch/7.x/wazuh-template.json
chmod go+r /etc/filebeat/wazuh-template.json
curl -s https://packages.wazuh.com/4.x/filebeat/wazuh-filebeat-0.4.tar.gz | tar -xvz -C /usr/share/filebeat/module
```

```bash
mkdir /etc/filebeat/certs
tar -xf ./wazuh-certificates.tar -C /etc/filebeat/certs/ ./$NODE_NAME.pem ./$NODE_NAME-key.pem ./root-ca.pem
mv -n /etc/filebeat/certs/$NODE_NAME.pem /etc/filebeat/certs/filebeat.pem
mv -n /etc/filebeat/certs/$NODE_NAME-key.pem /etc/filebeat/certs/filebeat-key.pem
chmod 500 /etc/filebeat/certs
chmod 400 /etc/filebeat/certs/*
chown -R root:root /etc/filebeat/certs
```

```bash
echo admin | /var/ossec/bin/wazuh-keystore -f indexer -k username
echo admin | /var/ossec/bin/wazuh-keystore -f indexer -k password
```

```bash
sudo vi /var/ossec/etc/ossec.conf

# <indexer>
#   <enabled>yes</enabled>
#   <hosts>
#     <host>https://0.0.0.0:9200</host>
#   </hosts>
#   <ssl>
#     <certificate_authorities>
#       <ca>/etc/filebeat/certs/root-ca.pem</ca>
#     </certificate_authorities>
#     <certificate>/etc/filebeat/certs/filebeat.pem</certificate>
#     <key>/etc/filebeat/certs/filebeat-key.pem</key>
#   </ssl>
# </indexer>
# 해당 부분의 host IP를 127.0.0.1로 변경해야 합니다.
```

```bash
systemctl daemon-reload
systemctl enable wazuh-manager
systemctl start wazuh-manager
```

<br><br>

##### Install wazuh-dashboard
###### `REF` : [Wazuh-dashboard Install Guide](https://documentation.wazuh.com/current/installation-guide/wazuh-dashboard/step-by-step.html)

```bash
apt-get install debhelper tar curl libcap2-bin #debhelper version 9 or later
apt-get -y install wazuh-dashboard
```

```bash
mkdir /etc/wazuh-dashboard/certs
tar -xf ./wazuh-certificates.tar -C /etc/wazuh-dashboard/certs/ ./$NODE_NAME.pem ./$NODE_NAME-key.pem ./root-ca.pem
mv -n /etc/wazuh-dashboard/certs/$NODE_NAME.pem /etc/wazuh-dashboard/certs/dashboard.pem
mv -n /etc/wazuh-dashboard/certs/$NODE_NAME-key.pem /etc/wazuh-dashboard/certs/dashboard-key.pem
chmod 500 /etc/wazuh-dashboard/certs
chmod 400 /etc/wazuh-dashboard/certs/*
chown -R wazuh-dashboard:wazuh-dashboard /etc/wazuh-dashboard/certs
```

```bash
systemctl daemon-reload
systemctl enable wazuh-dashboard
systemctl start wazuh-dashboard
```

<br><br>

##### Configure certificates

```bash
sudo /usr/share/wazuh-indexer/bin/opensearch-security-admin.sh --init
systemctl restart wazuh-indexer
```

### Connect Wazuh Server with Agent (with Sysmon)
<br><br>
![image](assets/img/edr-with-wazuh-sysmon-sigma/deploy_agent.png)
<br>
Wazuh Dashboard에서 Deploy new agent를 통해 Endpoint Agent를 생성합니다.

<br><br>
![image](assets/img/edr-with-wazuh-sysmon-sigma/created_agent.png)
생성된 Agent의 예시입니다.





