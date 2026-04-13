# Debian

- 사용 버전: 13 버전
- 하드웨어 지원이 잘 되기 때문에 개인 업무용 노트북, 개발환경 또는 여러 디스크의 연결이 필요없는 데스크탑에 사용합니다.
- 롤링 릴리즈 OS가 아니고 OpenZFS 처럼 강력한 파일시스템은 아니기 때문에 안정성이 필요로 하는 대규모 인프라에서는 사용하지 않습니다.
- 개발환경 자동화를 위해 사용합니다.
- amd64, arm64, riscv64를 지원합니다. FreeBSD보다 와이파이를 좀더 잘 지원합니다.

## 계보

```
Debian
├── Ubuntu (Canonical)
│   ├── Linux Mint
│   ├── Pop!_OS
│   ├── elementary OS
│   ├── Zorin OS
│   └── (수십 종의 *buntu 파생판)
├── Kali Linux
├── MX Linux
├── Raspberry Pi OS
├── Tails
└── Parrot OS
```

## add apt sources

Debian 리눅스 설치 이후 패키지 리포지토리 소스를 추가합니다.

```bash
vi /etc/apt/sources.list.d/debian.sources
```

하드웨어 펌웨어 바이너리가 non-free-firmware에 있습니다.

- GPU 드라이버 펌웨어: NVIDIA, AMD Radeon, Intel i915Wi-Fi
- 블루투스 펌웨어: Intel iwlwifi, Realtek rtl8xxxu, Broadcom
- NIC 펌웨어: Mellanox, Chelsio 등 고성능 NIC
- SSD/NVMe 컨트롤러 펌웨어일부: Samsung, SK하이닉스

```
Types: deb
URIs: https://deb.debian.org/debian
Suites: trixie trixie-updates
Components: main contrib non-free non-free-firmware
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg

Types: deb
URIs: https://security.debian.org/debian-security
Suites: trixie-security
Components: main contrib non-free non-free-firmware
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg

Types: deb
URIs: https://deb.debian.org/debian
Suites: trixie-backports
Components: main contrib non-free non-free-firmware
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
```

pkg를 인스톨 합니다.

```bash
apt update
apt upgrade
apt install -y htop vim neovim git mpv bat audacious nfs-common ffmpeg openimageio-tools curl rsync golang mpg123 gcolor3 sendmail mpack mutt vim-gtk3 libnotify-bin
apt install pandoc fonts-nanum texlive-xetex mdp
```

## 터미널 핫키 설정

설정 > 키보드 > 바로가기 > 사용자 바로가기

- Terminal

```
gnome-terminal
```

등록

## 터미널 비프음 제거

여러 사람이 모여 개발시 많은 비프음이 발생되기 때문에 기본적으로 비프음을 제거합니다.

```bash
sudo vim /etc/inputrc
```

```
set bell-style none # 21줄 주석제거하기
```

## 개발자를 위한 Git setting 설정

```bash
git config --global credential.helper store # git id,pw 저장
git config --global user.name "Username"
git config --global user.email id@lazypic.com
```


## Nvidia setting

필요시 Nvidia GPU 드라이버 다운로드 후 실행 권한 부여.

Debian 설치 후 부팅 시 GRUB 메뉴가 나타나면, 부팅할 커널 항목을 선택하고 `e` 키를 눌러 편집 모드로 들어갑니다.
linux 줄을 찾아서 끝에 systemd.unit=multi-user.target을 추가 후 F10 키를 누릅니다.

이후 아래 명령어를 이용해 패키지를 설치합니다.

```bash
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get install build-essential dkms
```

## mail client

메일 자동화를 위해 클라이언트를 썬더버드로 수정합니다. 터미널에서 아래 명령어를 타이핑합니다.

```bash
xdg-settings set default-url-scheme-handler mailto thunderbird.desktop
```

