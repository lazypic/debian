# Debian12

하드웨어 지원이 잘 되기 때문에 개인 업무용 노트북 또는 여러 디스크의 연결이 필요없는 데스크탑, 노트북등에서 사용합니다.
롤링 릴리즈 OS가 아니고 OpenZFS 처럼 강력한 파일시스템은 아니기 때문에 대규모 인프라에서는 사용하지 않습니다.

## add sources

```bash
vi /etc/apt/sources.list
```

```
deb http://deb.debian.org/debian bookworm main non-free-firmware
deb-src http://deb.debian.org/debian bookworm main non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security main non-free-firmware
deb-src http://deb.debian.org/debian-security/ bookworm-security main non-free-firmware

deb http://deb.debian.org/debian bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian bookworm-updates main non-free-firmware
```

install pkg

```bash
apt update
apt upgrade
apt install -y htop vim git mpv bat audacious nfs-common ffmpeg openimageio-tools curl rsync golang mpg123 gcolor3 sendmail mpack mutt
```
## 터미널 핫키

설정 > 키보드 > 바로가기 > 사용자 바로가기

- Terminal
- gnome-terminal

## 터미널 비프음 제거

```
sudo vim /etc/inputrc
```

```
set bell-style none # 21줄 주석제거하기
```

## 마운트방법

```bash
mount -t nfs 10.1.0.11:/home/jason/nfs /backup
```

## Crontab을 이용한 개인백업

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


## OpenVPN

Lazypic 관리자로부터 온 이메일 내부 VPN키를 /etc/openvpn/client.conf 이름으로 복사합니다.

```bash
sudo apt install openvpn
sudo cp ~/jason_lazypic_org.ovpn /etc/openvpn/client.conf
sudo systemctl start openvpn@client
sudo systemctl status openvpn@client
sudo systemctl stop openvpn@client
```
