# debian

```bash
apt update
apt upgrade
apt install -y htop vim git mpv bat audacious nfs-common ffmpeg openimageio-tools curl rsync golang nfs-common
```


## 개인백업

```bash
mount -t nfs 10.1.0.11:/home/jason/nfs /backup
```

crontab -e

```
0 * * * * rsync -avz --delete /home/jason /backup
```

## 암호제거

vim /etc/gdm3/daemon.conf

```
AutomaticLoginEnable = true
AutomaticLogin = jason
```

설정 > 개인정보 > 화면 > 자동화면 잠금 끄기
