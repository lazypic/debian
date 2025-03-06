# Debian12

하드웨어 지원이 잘 되기 때문에 개인 업무용 노트북 또는 여러 디스크의 연결이 필요없는 데스크탑, 노트북등에서 사용합니다.
롤링 릴리즈 OS가 아니고 OpenZFS 처럼 강력한 파일시스템은 아니기 때문에 대규모 인프라에서는 사용하지 않습니다.

amd64, arm64, riscv64를 지원합니다. FreeBSD보다 와이파이를 좀더 잘 지원합니다.

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
apt install -y htop vim neovim git mpv bat audacious nfs-common ffmpeg openimageio-tools curl rsync golang mpg123 gcolor3 sendmail mpack mutt vim-gtk3
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

## Git setting

```bash
git config --global credential.helper store # git id,pw 저장
git config --global user.name "Jason"
git config --global user.email jason@lazypic.org
```


## OpenVPN

Lazypic 관리자로부터 온 이메일 내부 VPN키를 /etc/openvpn/client.conf 이름으로 복사합니다.

```bash
sudo apt install openvpn
sudo cp ~/jason_lazypic_org.ovpn /etc/openvpn/client.conf
sudo systemctl start openvpn@client
sudo systemctl status openvpn@client
sudo systemctl stop openvpn@client
```

## Nvidia setting

드라이버 다운로드 후 실행 권한 부여.

Debian 부팅 시 GRUB 메뉴가 나타나면, 부팅할 커널 항목을 선택하고 e 키를 눌러 편집 모드로 들어가.
linux 줄을 찾아서 끝에 systemd.unit=multi-user.target을 추가 후 F10

```bash
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get install build-essential dkms
```

## mail client

```bash
xdg-settings set default-url-scheme-handler mailto thunderbird.desktop
```

