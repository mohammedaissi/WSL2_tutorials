# Docker Desktop Installation on Windows 10 Using WSL2

This is a complete guide written in Markdown to install and use Docker Desktop with WSL2 on Windows 10 Home or Pro.

---

## System Requirements

| Component            | Requirement                     | How to Check                             |
|---------------------|----------------------------------|------------------------------------------|
| Windows Version      | 2004 or newer                   | `winver`                                 |
| Architecture         | 64-bit                          | Settings → System → About                |
| RAM                  | 4 GB or more                    | Settings → System → About                |
| Virtualization       | Enabled in BIOS                 | `systeminfo | findstr /C:"Virtualization"` |
| WSL Version          | 2                               | `wsl -l -v`                              |
| Linux Distro         | Ubuntu 20.04 or later           | Microsoft Store                          |

---

## Enable WSL2

Open PowerShell as Administrator and run:

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Download and install the Linux kernel update:
https://aka.ms/wsl2kernel

Set WSL2 as the default version:

```bash
wsl --set-default-version 2
```

Install Ubuntu 20.04 from Microsoft Store.

Verify:

```bash
wsl -l -v
```

Convert distro to WSL2 if needed:

```bash
wsl --set-version Ubuntu-20.04 2
```

---

## Install Docker Desktop

Download from:
https://docs.docker.com/docker-for-windows/wsl/

Run the installer:
- Enable "Use WSL 2 instead of Hyper-V"
- Reboot if asked

---

## Docker Desktop Configuration

Open Docker Desktop → Settings:

**General**
- Enable “Use the WSL 2 based engine”

**Resources → WSL Integration**
- Enable integration with Ubuntu-20.04

---

## Verify Docker

Open Ubuntu WSL terminal:

```bash
docker version
docker info
docker run hello-world
```

Expected output includes:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

## Run Ubuntu Container

```bash
docker run -it ubuntu bash
```

Inside container:

```bash
apt update
apt install -y lsb-release
lsb_release -a
uname -a
```

Exit:

```bash
exit
```

---

## Common Docker Commands

| Task                     | Command                                    |
|--------------------------|--------------------------------------------|
| List running containers  | `docker ps`                                |
| List all containers      | `docker ps -a`                             |
| List images              | `docker images`                            |
| Start container          | `docker start <container_id>`             |
| Stop container           | `docker stop <container_id>`              |
| Remove container         | `docker rm <container_id>`                |
| Remove image             | `docker rmi <image_id>`                   |
| Run nginx on port 80     | `docker run -d -p 80:80 nginx`            |
| Clean unused data        | `docker system prune`                     |
| Enter running container  | `docker exec -it <container_id> bash`     |

---

## Troubleshooting

| Issue                            | Solution                                           |
|----------------------------------|----------------------------------------------------|
| Docker stuck on "Starting"       | Restart Docker service                             |
| Can't connect to daemon          | Ensure Docker Desktop is running                   |
| Network issues                   | Restart Docker, reset settings                     |
| Version still WSL1               | Use `wsl --set-version <distro> 2`                 |
| Reset Docker completely          | Docker Desktop → Troubleshoot → Reset to defaults  |

---

## References

- Docker with WSL2: https://docs.docker.com/docker-for-windows/wsl/
- WSL Docs: https://docs.microsoft.com/windows/wsl/
- WSL2 Kernel Update: https://aka.ms/wsl2kernel
- Ubuntu: https://www.microsoft.com/store/productId/9N6SVWS3RX71
- Docker Hub: https://hub.docker.com/
- WSL2 Announcement: https://devblogs.microsoft.com/commandline/wsl-2-is-now-available/

---
