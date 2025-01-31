# breadkun-compose

## 개요

`docker-compose` 레포지토리는 **백엔드 서비스(`ciabatta-core`)와 Nginx(`breadkun-nginx`) 컨테이너를 관리하며, 자동 배포 기능(CI/CD)을 포함**합니다.
이 프로젝트는 Docker Compose를 활용하여 컨테이너 실행을 간소화하고, GitHub Actions를 이용해 배포를 자동화합니다.

---

## 주요 기능

### 1. 환경 변수 주입

- `.env` 파일을 통해 컨테이너 실행 시 필요한 환경 변수를 동적으로 주입합니다.

### 2. 컨테이너 간 네트워크 구성

- `backend-network`(Bridge 네트워크)를 생성하여 컨테이너 간 통신을 지원합니다.
- 백엔드와 Nginx 간 트래픽을 내부 네트워크에서 처리하여 보안성과 성능을 향상합니다.

### 3. 호스트 머신의 파일을 컨테이너에 마운트

- Nginx 컨테이너가 호스트 루트의 SSL 인증서를 `/etc/letsencrypt` 디렉터리에서 읽어 사용할 수 있도록 읽기 전용으로 마운트합니다.
- 데이터 갱신 및 보안을 위해 필요한 파일들을 호스트에서 관리합니다.

---

## 배포 프로세스 (CI/CD)

이 프로젝트는 **GitHub Actions**를 사용하여 자동화된 배포를 수행합니다.

### 1. 환경 변수 (`.env`) 배포

1. `master` 브랜치에 코드가 푸시되면 **GitHub Actions**가 실행됩니다.
2. GitHub Secrets에서 환경 변수를 가져와 `.env` 파일을 생성합니다.
3. `.env` 파일을 원격 서버로 전송합니다.

### 2. Docker Compose 설정 파일 배포

1. `docker-compose.yaml` 파일을 서버로 전송합니다.
2. 기존 `docker-compose.yaml`을 삭제하고 새로운 파일을 적용합니다.
3. `docker-compose`를 재시작하여 새로운 설정을 반영합니다.

---

## Maintainer

- **HONG**
    - **Role**: Initial Developer & Current Maintainer
    - **GitHub**: [coldair426](https://github.com/coldair426)
    - **Blog**: [Velog](https://velog.io/@coldair426)
    - **Mail**: coldair426@gmail.com