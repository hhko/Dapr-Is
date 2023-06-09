# Dapr CLI 설치
> - Dapr CLI을 Dapr을 운영하기 위한 필수 도구입니다.
> - Dapr CLI 설치 PowerShell 스크립트
>   ```powershell
>   # 최신 버전과 기본 경로($Env:SystemDrive\dapr) 설치
>   iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 |
>   iex
> 
>   # 특정 버전과 특정 경로 설치
>   $Env:DAPR_INSTALL_VER = "<dapr_cli_version>"                # 예. $Env:DAPR_INSTALL_VER = "1.9.1"
>   $Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"       # 예. $Env:DAPR_INSTALL_DIR = "D:\dapr"
>   $script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
>   $block=[ScriptBlock]::Create($script)
>   Invoke-Command -ScriptBlock $block -ArgumentList "$Env:DAPR_INSTALL_VER", "$Env:DAPR_INSTALL_DIR"
>   ```
> - Dapr CLI 버전 이력 : [링크](https://github.com/dapr/cli/tags)

## 목차
- [x] Dapr CLI
- [x] Dapr CLI 설치
- [x] Dapr CLI 설치 세부내용
- [x] Dapr CLI 설치 확인
- [x] 참고 자료

<br/>

## Dapr CLI
- Dapr CLI은 Dapr Sidecar 관리합니다. 대표적인 관리 기능은 다음과 같습니다.  
  - Dapr와 함께 App. 실행하기 : Run an application with a Dapr sidecar.
  - Dapr 로그 확인하기 : Review sidecar logs.
  - Dapr 서비스 목록 확인하기 : List running services.
  - Dapr 대시보드 실행하기 : Run the Dapr dashboard.
- Dapr CLI은 Self-Hosted와 Kubernetes 환경에서 동작합니다.

<br/>

## Dapr CLI 설치
![](2023-03-26-14-14-10.png)

### 설치 방법
- PowerShell 스크립트 설치  
  `1.` Administrator 권한으로 최신 버전 설치하기  
  `2.` Administrator 권한으로 특정 버전 설차히기  
  `3.` Administrator 권한 없이 최신 버전 설치하기  
  `4.` Administrator 권한 없이 특정 버전 설차히기
- MSI 파일 설치

```powershell
# 1.1 Administrator 권한으로 최신 버전 설치하기 : Invoke-Expression
iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 |
iex

# 1.2 Administrator 권한으로 최신 버전 설치하기 : Invoke-Command
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block

# 2. Administrator 권한으로 특정 버전 설차히기
$Env:DAPR_INSTALL_VER = "<dapr_cli_version>"                # $Env:DAPR_INSTALL_VER = "1.9.1"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "$Env:DAPR_INSTALL_VER"

# 3. Administrator 권한 없이 최신 버전 설치하기
$Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"       # $Env:DAPR_INSTALL_DIR = "D:\dapr"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "", "$Env:DAPR_INSTALL_DIR"

# 4. Administrator 권한 없이 특정 버전 설차히기
$Env:DAPR_INSTALL_VER = "<dapr_cli_version>"                # $Env:DAPR_INSTALL_VER = "1.9.1"
$Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"       # $Env:DAPR_INSTALL_DIR = "D:\dapr"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "$Env:DAPR_INSTALL_VER", "$Env:DAPR_INSTALL_DIR"
```

#### `1.` Administrator 권한으로 최신 버전 설치하기
```powershell
# 최신 버전으로 기본 경로 설치
iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 |
iex

# 설치 과정
PS C:\Users\고형호> iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 |
>> iex

WARNING: Dapr is detected - C:\dapr\dapr.exe
CLI version: 1.10.0
Runtime version: n/a
Reinstalling Dapr...
Creating C:\dapr directory
Downloading https://api.github.com/repos/dapr/cli/releases/assets/95850842 ...
Extracting C:\dapr\dapr_windows_amd64.zip...
CLI version: 1.10.0
Runtime version: n/a
Clean up C:\dapr\dapr_windows_amd64.zip...
Try to add C:\dapr to User Path Environment variable...
Skipping to add C:\dapr to User Path - c:\dapr;C:\Users\고형호\.dapr\bin; ...

Dapr CLI is installed successfully.
To get started with Dapr, please visit https://docs.dapr.io/getting-started/ .
Ensure that Docker Desktop is set to Linux containers mode when you run Dapr in self hosted mode.
```
- 주요 내용 : install.ps1 파일을 다운로드 받아 실행합니다.
  - `iwr(Invoke-WebRequest) -useb` UTF8 형식으로 디코딩하지 않고 가져온 데이터를 바이너리 형식 그대로 반환합니다.
  - `iex(Invoke-Expression)` : Invoke-WebRequest에서 다운로드 받은 `install.ps1` 파일 내용을 평가(실행)합니다.

#### `2.` Administrator 권한으로 특정 버전 설차히기
```powershell
$Env:DAPR_INSTALL_VER = "<dapr_cli_version>"                # $Env:DAPR_INSTALL_VER = "1.9.1"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "$Env:DAPR_INSTALL_VER"
```
- 주요 내용 : install.ps1 파일을 다운로드 받아 인수를 전달하여 실행합니다.
  - `$Env:DAPR_INSTALL_VER` : 설치할 Dapr 버전을 명시해야 합니다.
  - `$script` : Invoke-WebRequest에서 UTF8 형식으로 디코딩하지 않고 가져온 `install.ps1` 파일 내용을 변수화합니다.
  - `$block` : `install.ps1` 파일 내용을 ScriptBlock으로 생성한니다.
  - `Invoke-Command` : ScriptBlock에 `ArgumentList`을 전달하여 평가(실행)합니다.

#### `3.` Administrator 권한 없이 최신 버전 설치하기
```powershell
$Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"       # $Env:DAPR_INSTALL_DIR = "D:\dapr"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "", "$Env:DAPR_INSTALL_DIR"
```
- `$Env:DAPR_INSTALL_DIR` : Administrator 권한 없이 제어할 수 있는 설치 경로를 명시해야 합니다.

#### `4.` Administrator 권한 없이 특정 버전 설차히기
```powershell
$Env:DAPR_INSTALL_VER = "<dapr_cli_version>"                # $Env:DAPR_INSTALL_VER = "1.9.1"
$Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"       # $Env:DAPR_INSTALL_DIR = "D:\dapr"
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
$block=[ScriptBlock]::Create($script)
Invoke-Command -ScriptBlock $block -ArgumentList "$Env:DAPR_INSTALL_VER", "$Env:DAPR_INSTALL_DIR"
```
- `$Env:DAPR_INSTALL_VER` : 설치할 Dapr 버전을 명시해야 합니다.
- `$Env:DAPR_INSTALL_DIR` : Administrator 권한 없이 제어할 수 있는 설치 경로를 명시해야 합니다.

### MSI 파일 설치
- [Darp 배포 사이트](https://github.com/dapr/cli/releases)에 방문하여 설치를 원하는 버전의 `dapr.msi` 파일을 다운로드 받습니다.  
  다운로드 받은 파을을 실행하여 설치를 진행합니다.

<br/>

## Dapr CLI 설치 세부내용
### PowerShell 스크립트 주요 내용
- 설치 스크리븥에서 사용하는 주요 PowerShell 함수
  - `iwr` : [Invoke-WebRequest](https://learn.microsoft.com/ko-kr/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.3)
  - `iex` : [Invoke-Expression](https://learn.microsoft.com/ko-kr/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.3)
  - `icm` : [Invoke-Command](https://learn.microsoft.com/ko-kr/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-7.3)
- 웹에서 다운로드 받은 ps1 파일을 인수 전달 없이 평가(실행)할 때는 `Invoke-Expression` 함수를 사용하면 됩니다.
  - 적용 사례
    - 최신 버전 설치
    - 기본 설치 경로
- 웹에서 다운로드 받은 ps1 파일을 인수를 전달하여 평가(실행)할 때는 `Invoke-Command` 함수를 사용하면 됩니다.
  - 적용 사례 : `-ArgumentList`
    - 특정 버전 설치 : 첫 번째 인수
    - 특정 설치 경로 : 두 번째 인수

### install.ps1 파일
- Dapr CLI 설치를 위한 PowerShell 스크립트 파일을 https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 사이트를 방문하면 확인할 수 있다.  
  `install.ps1` 설치 파일에서 중요하게 확인해야할 부분은 `param` 입니다. `param`에 설치할 버전과 설치할 경로를 전달받고 있습니다.
  ```powershell
  # https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1
  param (
    [string]$Version,                               # 설치할 Dapr CLI 버전
    [string]$DaprRoot = "$Env:SystemDrive\dapr",    # 설치할 Dapr CLI 설치 경로
    ...
  )

### install.ps1 파일 매개변수
- 설치할 버전은 첫 번째 매개변수에 전달합니다. 빈 문자열(예. "")면 최신 버전을 설치합니다.  
  특정 버전을 설치하기 위해 Dapr CLI 버전은 [Dapr CLI GitHub Tags](https://github.com/dapr/cli/tags)을 방문하여 확인할 수 있습니다.  
  버전을 확인하였으면 install.ps1 파일 실행을 위한 `-ArgumentList`의 첫 번째 아규먼트로 입력합니다.
  ```shell
  # 최신 버전을 설치합니다.
  #  - 첫 번째 인수(버전) : ""
  invoke-command -ScriptBlock $block -ArgumentList ""

  # 특정 버전(v1.9.1)을 설치합니다.
  #  - 첫 번째 인수(버전) : "1.9.1"
  invoke-command -ScriptBlock $block -ArgumentList "1.9.1"
  ```
- 설치할 경로는 두 번째 매개변수 `[string]$DaprRoot = "$Env:SystemDrive\dapr"` 기본 값으로 시스템 드라이브(예. $Env:SystemDrive : C:) `dapr` 폴더에 설치를 진행합니다.  
  시스템 드라이브에 대한 권한이 없거나 또는 다른 드라이브의 경로에 설치를 원하면 두번째 매개변수 값으로 전달하면 됩니다.  
  ```powershell
  # 설치할 폴더 경로를 DAPR_INSTALL_DIR 환경 벼눗에 추가합니다.
  $Env:DAPR_INSTALL_DIR = "<your_alt_install_dir_path>"

  # 최신 버전을 특정 경로에 설치합니다.
  #  - 첫 번째 인수(버전) : ""
  #  - 두 번째 인수(경로) : "$Env:DAPR_INSTALL_DIR"
  invoke-command -ScriptBlock $block -ArgumentList "", "$Env:DAPR_INSTALL_DIR"

  # 특정 버전(v1.9.1)을 특정 경로에 설치합니다.
  #  - 첫 번째 인수(버전) : "1.9.1"
  #  - 두 번째 인수(경로) : "$Env:DAPR_INSTALL_DIR"
  invoke-command -ScriptBlock $block -ArgumentList "1.9.1", "$Env:DAPR_INSTALL_DIR"
  ```

### PowerShell 환경 변수 
- `$Env:SystemDrive`은 시스템 드라이브를 확인할 수 있는 PowerShell 변수입니다.
  ```shell
  # Cmd에서 시스템 드라이브 확인하기
  C:\>powershell $Env:SystemDrive
  C:
  ```
  ```powershell
  # PowerShell에서 시스템 드라이브 확인하기
  PS C:\> $Env:SystemDrive
  C:
  ```

<br/>

## Dapr CLI 설치 확인
- Shell(Cmd, PowerShell)에서 `dapr -v`을 입력하면 Dapr CLI 설치를 확인할 수 있습니다.
  ```powershell
  PS C:> dapr -v
  CLI version: 1.10.0
  Runtime version: n/a
  ```

<br/>

## 참고 자료
- [x] [Install the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/)
- [x] [Steps to upgrade Dapr in a self-hosted environment](https://docs.dapr.io/operations/hosting/self-hosted/self-hosted-upgrade/)
- [x] [Uninstall CLI command reference](https://docs.dapr.io/reference/cli/dapr-uninstall/)
- [x] [Uninstall Dapr in a self-hosted environment](https://docs.dapr.io/operations/hosting/self-hosted/self-hosted-uninstall/)
