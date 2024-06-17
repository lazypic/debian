# debian

```bash
apt update
apt upgrade
apt install -y htop vim git mpv bat audacious nfs-common ffmpeg openimageio-tools curl rsync golang
```



```bash
apt install nfs-common
mount -t nfs 10.1.0.11:/home/jason/nfs /backup
```

crontab -e

```
0 * * * * rsync -avz --delete /home/jason /backup
```
