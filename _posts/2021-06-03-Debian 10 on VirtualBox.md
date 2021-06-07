---
title: Debian 10 on VirtualBox
excerpt: 가상머신에 데비안 서버 올려보기
categories: 
  - OS
---

## Summary

(작성중)

## Introduction

가상화에 대해서 알아보고자 가상머신에 Debian을 올려보았습니다.
VirtualBox에 가상머신을 만들고 기본적인 설정을 마치는 것이 목표입니다.
간단한 서비스도 한번 올려보도록 하겠습니다.

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

[TEST](https://www.makeuseof.com/tag/reasons-choose-debian-linux/)

## What have you learnd?

### LVM

> Logical Volume을 효율적이고 유연하게 관리하기 위한 커널의 한 부분이자 프로그램.

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

> AppArmor는 시스템 관리자가 프로그램 프로필 별로 프로그램의 역량을 제한할 수 있게 해주는 
리눅스 커널 보안 모듈이다.

> UFW(Uncomplicated Firewall)는 데비안 계열 및 다양한 리눅스 환경에서 사용하는 
방화벽 관리 프로그램이다.

AppArmor는 기본적으로 활성화, UFW는 설치 후 활성화해야 합니다.
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

> SSH(Secure Shell)은 네트워크 상의 다른 컴퓨터에 로그인하거나 
원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있게 해주는 
응용 프로그램 또는 그 프로토콜 입니다.

데비안을 가상머신에 성공적으로 설치한 후, SSH를 통해 접속했습니다.
보안을 위해 22번 포트가 아닌 다른 포트를 사용했습니다.

UFW에서 포트를 열어 외부에서 접속할 수 있게 했습니다.
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

### Monitoring

cron

## BONUS

### partitioning

### WordPress + lighttpd + MariaDB + PHP

## Conclusion