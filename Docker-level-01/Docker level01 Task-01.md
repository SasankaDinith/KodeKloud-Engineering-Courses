# Task01: Install Docker Packages and Start Docker Service
The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team.<br/>
They intend to conduct testing with the following steps:<br/><br/>
Install docker-ce and docker compose packages on App Server 3 
<br/>
Initiate the docker service.


---

## Answer

### 1. Remove old Docker versions
```bash
sudo yum remove -y docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine || true
```

### 2. Install prerequisites
```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

### 3. Add Docker repository
```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### 4. Install Docker CE and Compose plugin
```bash
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 5. Start and enable Docker service
```bash
sudo systemctl enable --now docker
sudo systemctl status docker --no-pager
```

### 6. Verify installation
```bash
sudo docker run --rm hello-world
docker --version
docker compose version
```

---

## Optional: Add user to Docker group
```bash
sudo usermod -aG docker $USER
```
Log out and back in for changes to take effect.

---

## Troubleshooting Tips
- **Service fails to start**: Check logs using `journalctl -u docker --no-pager`.
- **Firewall / proxies**: Configure Docker daemon in `/etc/systemd/system/docker.service.d/proxy.conf` if behind a proxy.

