---
title: Debian 10 on VirtualBox
excerpt: 가상머신에 데비안 서버 올려보기
categories: 
  - OS
---

## Summary

가상화에 대해서 알아보고자 가상머신에 `Debian`을 설치했습니다.
`VirtualBox`에 가상머신을 만들고 기본적인 설정을 마치는 것이 목표입니다.
이를 통해 데비안과 혹은 운영체제에 대해서 학습했습니다.

설정을 마치고 간단한 웹 서비스도 만들었습니다.
`LAMP` 에서 `Apache` 만 `lighttpd` 로 바꿔서 설치했습니다.
서비스를 운영하는 것이 목적이 아니라서, `WordPress` 의 작동여부만 확인했습니다.

진행하면서 필요하다고 생각하는 부분을 정리했습니다.
깊게 들어가면 어려운 개념이 많아서 최대한 큰 흐름을 이해하려고 노력했습니다.

다 작성하고 보니 가상화에 대한 내용보다 `Debian`에 대한 내용이 많았습니다.
그래서 가상화에 대한 내용은 다음에 따로 다루도록 하겠습니다.

## Introduction

전세계 수많은 기업이 웹 서버를 다양한 운영체제에서 운영하고 있습니다.
어떤 웹 서버를 쓸지 혹은 어떤 운영체제를 쓸지는 각자의 장단점이 있습니다.

운영체제에 대한 이해는 개발자라면 피해갈 수 없는 주제입니다.
좋은 성능을 가진 프로그램을 개발하려면 실제 어떻게 실행되는지 이해하고 있어야합니다.

다양한 운영체제를 모두 다 이해할 수는 없지만, 최소한 한가지 운영체제는 잘 알고 싶었습니다.
저는 개발환경으로 `Ubuntu` 를 사용하고 있습니다.
`Ubuntu` 는 `Debian` 을 기반으로 만든 운영체제 입니다.

저는 `Ubuntu` 를 더 잘 이해하기 위해 `Debian` 을 살펴봤습니다.
그래서 `Debian` 을 가상머신에 설치하고 여러가지 설정을 통해 이해를 넓혔습니다.

## What is Debian?

> CULTURE Origin of the Debian name
> Look no further: Debian is not an acronym.
This name is, in reality, a contraction of two first names: that of Ian Murdock, and his girlfriend at the time, 
Debra. Debra + Ian = Debian.

Debian은 GNU/Linux 배포판입니다.
리눅스 커널과 무료 소프트웨어에 기반을 둔, 설치 및 관리를 위한 소프트웨어와 시스템을 포함한 완전한 운영체제입니다.
*Debian Manifesto*를 보면 Debian의 명확한 목표를 알 수 있습니다.

- quality: Debian would be developed with the greatest care, to be worthy of the Linux kernel
- It would also be a non-commercial distribution, sufficiently credible to compete with major commercial distributions.

### A Multy-Platform Opeating System

초기 원칙에 충실한 Debian은 많은 성공을 거두어 오늘날 엄청난 규모에 도달했습니다.
현재 공식적으로 지원하는 10개의 하드웨어 아키텍처와 FreeBSD와 같은 다른 커널이 있습니다.
더 나아가, 28,000개의 패키지를 통해 사용 가능한 소프트웨어는 가정과 기업에서 가지고 있는 모든 요구사항을 충족할 수 있습니다.

### The Quality of Free Software

데비안은 무료 소프트웨어의 모든 원칙을 따르며 새 버전은 준비가 될 때까지 출시되지 않습니다.
개발자는 정해진 일정에 따라 작업하지 않으며 임의의 기한을 맞추기 위해 서두를 필요가 없습니다.

데비안은 품질에 타협하지 않습니다.
패키지의 알려진 모든 중요한 버그는 새로운 버전에서 해결됩니다.
이 경우 초기 예측 릴리즈 날짜를 뒤로 밀어야하는 경우에도 마찬가지 입니다.
중요한 버그가 수정되지 않아 품질 요구 사항을 충족하지 않는 선택적 패키지는 안정 릴리즈에서 삭제합니다.

### The Legal Framework: A Non-Profit Organization

법적으로 Debian은 미국의 비영리 자원 봉사 협회가 관리하는 프로젝트 입니다.
프로젝트는 약 천명의 Debian 개발자를 가지고 있지만, 더 많은 기여자들이 있습니다.

## Why choose Debian?

1. Debian is Stable and Depenable.
2. You can use each version for a long time.
3. Debian is ideal for server.
4. A rolling release option is available.
5. Debian supports many PC architecture.
6. Debian has great software support.
8. You want to be close to the source.
9. You can install a free software only version.
10. Few Linux distros have lived as long ad debian.
11. You don't need a strong internet connection.
12. Debian is desktop agnostic.

## What have you learnd?

### LVM

> LVM, Logical Volume Manger는 Logical Volume을 효율적이고 유연하게 관리하기 위한 커널의 한 부분이자 프로그램이다.

> 디스크나 대용량 스토리지 장치를 유연하고 확장이 가능하게 다룰 수 있는 기술이며 이를 커널에 구현한 기술을 LVM이라고 한다.

기존 방식이 파일시스템을 블록 장치에 직접 접근해서 읽고 쓰기를 했다면,
LVM은 파일시스템이 LVM이 만든 가상의 블록 장치에 읽고 쓰기를 합니다.

직접 물리 스토리지를 사용하는 것보다 다양한 측면에서 유연성을 제공하는데,
유연한 용량 조절, 크기 조정이 가능한 스토리지 풀(Pool), 
편의에 따른 장치 이름 지정, 디스크 스트라이핑, 미러 볼륨 등을 제공합니다.

LVM 은 이름처럼 파티션대신 볼륨이라는 단위로 저장 장치를 다룰 수 있으며, 
물리 디스크를 볼륨 그룹으로 묶고 이것을 논리 볼륨으로 분할하여 관리합니다. 
스토리지의 확장이나 변경시 서비스의 변경을 할 수 있으며 
특정 영역의 사용량이 많아져서 저장 공간이 부족할 경우에 유연하게 대응할 수 있습니다.

### Dpkg and Differences between aptitude and apt

> `dpkg` - package manager for Debian. `dpkg` is a tool to install, build, remove and manage Debian packages.
The primary and more user-friendly front-end for dpkg is aptitude. 

> `apt` provides a high-level cammandline interface for the package management system.
pakage management system that handles the installation of Debian package on Debian-based Linux distribution.

> `aptitude` is an Ncureses and command-line based front-end to numerous apt libraries, 
which are also used by apt, the default Debian package manager.

데비안 패키지는 기본적으로 `dpkg`를 통해 설치할 수 있습니다.
하지만 의존성을 사용자가 직접 해결해야합니다.

`apt`는 복잡한 의존성과 패키지 설치를 간단하게 해주는 프로그램입니다.
CLI로 명령을 입력하면 패키지 설치, 삭제 그리고 변경을 손쉽게 할 수 있습니다.

`aptitude`는 CLI로 사용하는 `apt`에 UI를 추가한 프로그램입니다.
내부적으로 apt를 사용하지만, UI가 있으므로 훨씬 사용자 친화적입니다. 

저는 익숙한 `apt`를 사용하지만, 앞으로는 `aptitude`를 사용하는 것도 좋아보입니다.

### AppArmor and UFW

> `AppArmor`는 시스템 관리자가 프로그램 프로필 별로 프로그램의 역량을 제한할 수 있게 해주는 
리눅스 커널 보안 모듈이다.

> `UFW`(Uncomplicated Firewall)는 데비안 계열 및 다양한 리눅스 환경에서 사용하는 
방화벽 관리 프로그램이다.

`AppArmor`는 기본적으로 활성화, `UFW`는 설치 후 활성화해야 합니다.
두 프로그램 모두 관리자 권한이 필요합니다.

```shell
# AppArmor
sudo aa-status

# UFW
sudo apt install ufw
sudo ufw enable
sudo ufw status
```

### SSH

> `SSH`(Secure Shell)은 네트워크 상의 다른 컴퓨터에 로그인하거나 
원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있게 해주는 
응용 프로그램 또는 그 프로토콜 입니다.

데비안을 가상머신에 성공적으로 설치한 후, SSH를 통해 접속했습니다.
보안을 위해 22번 포트가 아닌 다른 포트를 사용했습니다.

`UFW`에서 포트를 열어 외부에서 접속할 수 있게 했습니다.
가상머신에 접속하기 위해서 포트포워딩을 사용했습니다.

```shell
sudo ufw enable
sudo ufw allow 4242
```

```shell
ssh 'user'@'host_ip' -p 4242
```

### User and Group

시스템 관리자의 중요한 역할 중 하나는 사용자를 관리하는 것입니다.
사용자를 만들고, 그룹에 추가하거나 그룹을 만드는 명령을 확인했습니다.

```shell
useradd {user} -G {group}
passwd {user}
```

```shell
usermod -aG {group1, group2, group3, ...} {user}
# or
gpasswd -a {user} {group}

groups {user}
```

```shell
groupadd {group name}
```

### Password policy

보안을 위해 다음과 같은 강력한 비밀번호 정책을 만들었습니다.

- 비밀번호는 30일마다 만료됩니다.
- 비밀번호를 바꾸려면 최소 2일을 기다려야 합니다.
- 사용자는 비밀번호가 만료되기 최소 7일 전에 경고 메세지를 받아야 합니다.
- 비밀번호의 최소 길이는 10입니다.
- 비밀번호는 최소 한개의 대문자와 숫자를 포함해야 하고, 3개의 연속적인 동일한 문자를 포함할 수 없습니다.
- 비밀번호는 사용자의 이름을 포함할 수 없습니다.
- 비밀번호는 이번 비밀번호의 일부분이 아닌 문자를 최소 7자 가지고 있어야 합니다.
- 관리자 비밀번호도 위의 정책을 지켜야합니다.

정책을 적용하기 위해서 `/etc/login.def` 파일을 수정하고, 
`libpam-pwquality` 패키지를 설치했습니다.

`chage` 명령을 통해 사용자의 비밀번호 만료 정보를 확인할 수 있습니다.
그리고 `--maxdays, --mindays, --warndays` 를 통해 정보를 수정할 수 있습니다.

```shell
chage -l {user}
```

`/etc/login.def` 파일을 수정하면 기본 만료 정보를 설정할 수 있습니다.

- PASS_MAX_DAYS
- PASS_MIN_DAYS
- PASS_WARN_DAYS

`/etc/pam.d/common-password` 파일을 수정하여 안전한 비밀번호를 위한 규칙을 설정했습니다.
`pam_pwquality.so retry=3` 뒤로 다음과 같은 항목을 작성했습니다.

- minlen=10
- ucredit=-1
- dcredit=-1
- maxrepeat=3
- usercheck=1
- difok=7
- enforce_for_root

### Configuration for sudo group

sudo를 사용하기 위해서는 설치해야 합니다.
그리고 sudo를 사용하는 계정이 sudo 그룹에 속해 있어야 합니다.

```shell
# 최고 관리자 계정
apt install sudo
usermod -aG sudo {user}
```

관리자(sudo) 그룹 또한 강력한 정책을 만들었습니다.

- sudo를 사용한 인증은 비밀번호를 잘못 입력했을 경우 시도를 3회로 제한합니다.
- sudo를 사용할 때 비밀번호를 잘못 입력하여 오류가 발생하면 사용자 지정 메세지를 표시합니다.
- sudo를 사용한 각 작업은 입력과 출력 모두를 저장해야 합니다. 로그 파일의 경로는 /var/log/sudo/ 폴더입니다.
- 보안상의 이유로 `TTY` 모드가 켜져있어야 합니다.
- 마찬가지 보안상의 이유로 sudo에서 사용할 수 있는 경로를 제한합니다.

```shell
# 최고 관리자 계정
visudo

# 편집기에서 아래의 내용 추가
Defaluts  passwd_tries=3
Defaults  badpass_message="user custom message."
Defaults  logfile="/var/log/sudo/sudo.log"
Defaults  requiretty
Defaults  secure_path="..."
```

### Monitoring

시스템 관리자의 또 다른 역할 중 하나는 모니터링 입니다.
여러가지 모니터링이 있지만, 여기서는 자원을 모니터링 했습니다.
모니터링 한 자원은 다음과 같습니다

- 운영체제의 아키텍쳐와 커널 버전
- 물리 프로세서의 수
- 가상 프로세서의 수
- 서버에서 사용 가능한 RAM 및 사용률
- 서버에서 사용 가능한 메모리 및 사용률
- 마지막 재부팅 날짜 및 시간
- LVM이 활성 상태인지 여부
- 활성화 된 연결 수
- 서버를 사용하는 사용자 수
- 서버의 IPv4 주소와 MAC 주소
- sudo 프로그램으로 실행한 명령 수

![monitoring](/assets/images/posts/2021-06-03-Debian 10 on VirtualBox/monitoring.png)

위의 자원을 조회할 수 있는 [Shell script]()를 작성했습니다.
그리고 `crontab` 을 사용해서 매 10분마다 주기적으로 조회할 수 있도록 했습니다.
마지막으로, `wall`을 통해 로그인한 사용자에게 메세지를 보냈습니다.

> 소프트웨어 유틸리티 `cron` 은 유닉스 계열 컴퓨터 운영 체제의 시간 기반 잡 스케줄러다.

> 소프트웨어 환경을 설정하고 관리하는 작업을 고정된 시간, 날짜 간격에 주기적으로
실행할 수 있도록 스케줄링 하기 위해 `cron`을 사용한다.

> `wall` display a message, or the content of file, or otherwise its standard input, 
on the terminals of all currently logged in users.

```shell
# 최고 관리자 계정
crontab -e

# 맨 밑에 한 줄 추가
*/10 * * * * bash monitoring.sh | wall 
```

## BONUS

웹 서버를 설치하고 간단한 서비스를 만들었습니다.
웹 서버는 기존에 설치한 `Apache` 를 지우고 `lighttpd` 를 사용하여 구성했습니다.
`LAMP` 에서 서버만 `lighttpd` 로 바꿔서 구성했습니다.

`MariaDB` 와 `PHP` 를 활용할 수 있는 서비스로 `WordPress` 를 선택했습니다.
마지막으로, `phpMyAdmin` 을 설치했습니다. 데이터베이스를 조작해보고 잘 작동하는 것 까지만 확인했습니다.

추가적인 서비스를 계속해서 추가할 수 있지만, 주제에서 벗어난다고 생각했습니다.
그래서 여기까지만 진행했습니다.

## Conclusion

가상머신에 `Debian`을 설치하고 기본적인 설정을 끝냈습니다.
`SSH` 를 통한 원격접속과 `WordPress` 를 이용한 간단한 서비스도 구현했습니다.
설정을 하면서 모르는 부분을 정리하고 아는 부분은 다시 배웠습니다.

가상머신의 가상화 기술보다 운영체제를 공부했습니다.
아마 가상화 관련 내용은 이 후 도커나 쿠버네티스를 하게 되면 거기서 자세히 다룰 것 같습니다.

시스템 관리자의 막강한 권한을 다루는 설정을 하면서
"강력한 힘에는 막중한 책임이 따른다." 라는 말이 생각났습니다.
무작정 사용했던 `sudo` 가 얼마나 강력한 힘을 가지고 있는지 배웠습니다.

애플리케이션 개발만 하다가 이런 부분을 학습하고 나니 확실이 견문이 넓어졌습니다.
개발환경 세팅이 편하다는 이유로 우분투를 사용하고 있습니다.
우분투 또한 데비안 계열이므로 학습한 내용이 모두 유익했습니다.
단순히 사용자 입장이 아닌 관리자의 입장으로 운영체제를 이해할 수 있었습니다.

다음에는 도커와 쿠버네티스를 학습하면서 
가상화 기술과 컨테이너 기반 개발에 대해서 다뤄보도록 하겠습니다.

## Reference

- [The Debian 10 Administrator's Handbook](https://www.debian.org/doc/manuals/debian-handbook/the-debian-project.en.html#sect.what-is-debian)
- [12 Reasons why should you choose Debian Linux](https://www.makeuseof.com/tag/reasons-choose-debian-linux/)
- [Logical Volumn Manager HOWTO](https://wiki.kldp.org/wiki.php/DocbookSgml/LVM-HOWTO)
- [Linux man pages](https://linux.die.net/man/)
- ...