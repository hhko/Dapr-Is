# Dapr CLI 업그레이드

- [ ] [Steps to upgrade Dapr in a self-hosted environment](https://docs.dapr.io/operations/hosting/self-hosted/self-hosted-upgrade/)

## 목차
- [ ] Dapr CLI 업그레이드

## Dapr CLI 업그레이드
```shell
# Darp CLI 제거
dapr uninstall --all

# Dapr CLI 최신 버전 설치
iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 |
iex

# Dapr CLI 버전 확인
dapr -v
```