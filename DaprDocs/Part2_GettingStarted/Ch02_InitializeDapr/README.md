# Dapr 초기화 
> Initialize Dapr in your local environment

## 목차
- ...

<br/>

## 요약
- ...


## Dapr 초기화 과정
- Dapr 초기화 작업을 수행하면 관련 컨테이너를 다운로드 받아 실행하고 컴포넌트 정의 폴더를 생성합니다.
  - `dapr_redis` : 로컬 상태 저장과 메시지 브로커을 위한 Redis 컨테이너 인스턴스를 실행합니다.
  - `dapr_zipkin` : Observability(관찬 가능성)을 위한 Zipkin 컨테이너 인스턴스를 실행합니다.
  - `dapr_placement` : 로컬 액터 모데을 위한 Dapr placement service 컨테이너 인스턴스를 실행합니다.
  - `%UserProfile%/.dapr` : 컴포넌트 정의를 위한 기본 폴더를 생성합니다.

<br/>

## Dapr 초기화 명령
```shell
# Windows Terminal을 관리자 권한으로 실행(Run as administrator)합니다.
PS C:\> dapr init
```

![](2023-03-27-23-46-21.png)

`explorer "%UserProfile%\.dapr\"`

![](2023-03-27-23-49-02.png)

<br/>

## 참고 자료
- [ ] [Initialize Dapr in your local environment](https://docs.dapr.io/getting-started/install-dapr-selfhost/)