#### 安装命令

1. nezha.sh脚本文件恢复
```bash
cd /root
wget https://raw.githubusercontent.com/honorcnboy/nezhav0/refs/heads/main/nezha.sh
chmod 711 nezha.sh
```

2. agent文件安装
```bash
mkdir -p /opt/nezha/agent
chmod 700 /opt/nezha /opt/nezha/agent

2.1 AMD
wget https://raw.githubusercontent.com/honorcnboy/nezhav0/refs/heads/main/nezha-agent-amd
mv nezha-agent-amd /opt/nezha/agent/
chmod 755 /opt/nezha/agent/nezha-agent

2.2 ARM
wget https://raw.githubusercontent.com/honorcnboy/nezhav0/refs/heads/main/nezha-agent-arm
mv nezha-agent-arm /opt/nezha/agent/
chmod 755 /opt/nezha/agent/nezha-agent
```

3. service文件安装
```bash
wget https://raw.githubusercontent.com/honorcnboy/nezhav0/refs/heads/main/nezha-agent.service
sudo mv nezha-agent.service /etc/systemd/system/
chmod 600 /etc/systemd/system/nezha-agent.service

sudo sed -i 's|ExecStart=/opt/nezha/agent/nezha-agent "-s" "web/ip:8888" "-p" "123456789" --disable-auto-update --disable-force-update|ExecStart=/opt/nezha/agent/nezha-agent "-s" "123.123.123.123:5555" "-p" "qwertyuiop123456" --disable-auto-update --disable-force-update|g' /etc/systemd/system/nezha-agent.service
- 123.123.123.123:5555 ：替换为你自己的【网址:端口】或是【IP:端口】
- qwertyuiop123456：替换为相对应的密钥
```

4. 启动服务
```bash
systemctl daemon-reload
systemctl enable nezha-agent
systemctl start nezha-agent
```
