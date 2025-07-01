# GCP에 Spring Boot Docker 이미지 배포 가이드 (macOS & Windows)

## 0단계: GCP 준비 (무료 VM + 프로젝트)

### ✅ GCP 프로젝트 생성
1. [GCP 콘솔 접속](https://console.cloud.google.com/)
2. 상단 바 → **프로젝트 선택 > 새 프로젝트 만들기**
3. 원하는 이름 지정 후 생성

---

### ✅ 무료 VM 인스턴스 생성 (f1-micro)
1. GCP 콘솔 → **Compute Engine > VM 인스턴스**
2. "인스턴스 만들기" 클릭
3. 아래 옵션 설정:

| 항목         | 설정값                                                        |
| ------------ | ------------------------------------------------------------- |
| 이름         | 원하는 이름 (예: `spring-vm`)                                 |
| 리전         | `us-west1` 또는 `us-central1` *(무료 티어 대상 지역)*         |
| 머신 유형    | **E2 또는 f1-micro** (※ `f1-micro`는 `us-*` 리전에서만 무료) |
| 부팅 디스크  | Debian 11 이상                                               |
| 방화벽       | ✅ **HTTP 트래픽 허용** 체크                                   |
| 외부 IP      | 자동 (기본값 유지)                                           |
| 액세스 범위  | **모든 Cloud API 전체 액세스 허용** (Secret Manager 등 사용시) |

> **Tip:**
> - 무료 티어를 원한다면 반드시 `us-west1`, `us-central1` 등 미국 리전을 선택하세요.
> - VM 인스턴스 생성 시 "방화벽: HTTP 트래픽 허용"을 꼭 체크하세요.  
> - HTTP 트래픽 허용을 체크하면 80번 포트가 자동으로 방화벽에 열립니다.
> - "액세스 범위"에서 "모든 Cloud API에 대한 전체 액세스 허용"을 선택하면 Secret Manager 등 모든 GCP API를 사용할 수 있습니다.
> - 이미 생성된 인스턴스라면, 인스턴스 중지 → 수정 → 위 옵션들 체크/설정 후 저장하세요.
> - VM 생성 후 외부 IP 주소를 꼭 메모해두세요! (배포 후 접속에 필요)

---

## 1단계: Dockerfile 작성 (프로젝트 루트 디렉토리)
- 프로젝트 루트에 `Dockerfile`을 작성

```dockerfile
# 예시 Dockerfile
FROM openjdk:21-ea-oraclelinux8
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

## 2단계: JAR 파일 생성
- 각 운영체제에 맞는 명령어를 실행

**macOS / Linux:**
```bash
# 실행 권한이 없는 경우에만 최초 1회 실행
chmod +x mvnw

# 프로젝트 클린 및 패키징 (JAR 파일 생성)
./mvnw clean package
```

**Windows (CMD 또는 PowerShell):**
```bash
.\\mvnw.cmd clean package
```

## 3단계: Docker 이미지 빌드 및 Push

### [A] 멀티 아키텍처 이미지가 필요할 때 (Mac, ARM, 여러 환경 지원)
- Mac(M1/M2), ARM 서버, 다양한 환경에서 사용할 이미지를 만들고 싶을 때 사용
- 운영체제 상관없이 아래 명령어를 사용하기
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t <your-dockerhub-username>/<your-image-name>:latest . --push
```

### [B] 단일 아키텍처(Windows/amd64)만 필요할 때 (가장 일반적인 Windows 환경)
- GCP 서버가 amd64(x86)이고, 내 PC도 amd64(Windows)라면 아래 명령어만으로 충분함.
- Windows/macOS/Linux 모두 동일하게 사용 가능
```bash
docker build -t <your-dockerhub-username>/<your-image-name>:latest .
docker push <your-dockerhub-username>/<your-image-name>:latest
```

> **Tip:**
> - GCP VM이 amd64(x86) 아키텍처라면 단일 아키텍처 빌드로 충분함.
> - 여러 환경(ARM, Mac 등)에서 동일 이미지를 쓰고 싶다면 멀티 아키텍처 빌드를 추천함.

## 4단계: GCP VM에서 컨테이너 실행

### 1. VM에 Docker 설치 (VM 생성 후 최초 1회만)
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

### 2. Docker 로그인 (VM에서)
```bash
docker login -u <your-dockerhub-username>
```

### 3. Docker 이미지 가져오기
```bash
sudo docker pull <your-dockerhub-username>/<your-image-name>:latest
```

### 4. 컨테이너 실행 (가장 중요한 포트 매핑!)
```bash
docker run -d -p <호스트 포트>:<컨테이너 포트> <your-dockerhub-username>/<your-image-name>:latest
```

`docker run` 명령어의 `-p` 옵션은 `-p <호스트 포트>:<컨테이너 포트>` 형식

- **`<컨테이너 포트>`**: Spring Boot 애플리케이션이 사용하는 포트 (`application.properties`의 `server.port`)
- **`<호스트 포트>`**: 외부에서 GCP 서버에 접속할 때 사용할 포트 (보통 80번을 사용)

#### 예시 1: `server.port=8080` 일 때 (가장 일반적인 경우)
- Spring Boot 애플리케이션이 **8080 포트**를 사용.
- 외부에서는 표준 HTTP 포트인 **80번**으로 접속하게 하고 싶을 때.
```bash
sudo docker run -d -p 80:8080 <your-dockerhub-username>/<your-image-name>:latest
```
- **접속 방법**: `http://<GCP 외부 IP>` (포트 번호 생략 가능)

#### 예시 2: `server.port=8083` 이고, `local` 프로필을 활성화 할 때
- Spring Boot 애플리케이션이 `local` 프로필에서 **8083 포트**를 사용.
- 외부 접속은 똑같이 **80번** 포트를 사용.
```bash
sudo docker run -d -p 80:8083 -e SPRING_PROFILES_ACTIVE=local <your-dockerhub-username>/<your-image-name>:latest
```
- **`-e SPRING_PROFILES_ACTIVE=local`** : 컨테이너 환경 변수를 설정하여 `local` 프로필을 강제로 활성화함.
- **접속 방법**: `http://<GCP 외부 IP>`

## 5단계: GCP 방화벽 설정 (외부 접속 허용)
1. GCP 콘솔 접속: https://console.cloud.google.com/
2. 네트워크 → VPC 네트워크 → 방화벽 규칙 이동
3. "방화벽 규칙 만들기" 클릭
4. 아래 내용으로 설정:

| 항목 | 값 | 설명 |
| :--- | :--- | :--- |
| 이름 | `allow-http-80` (또는 원하는 이름) | 규칙을 식별하기 쉬운 이름 |
| 네트워크 | `default` (또는 VM이 속한 네트워크) | |
| 트래픽 방향 | `수신` | 외부에서 서버로 들어오는 트래픽 |
| 소스 IP 범위 | `0.0.0.0/0` | 모든 IP 주소에서의 접속을 허용 |
| 프로토콜 및 포트 | **지정된 프로토콜 및 포트** 선택 후 `tcp:80` 입력 | Docker의 **호스트 포트**와 일치시켜야 함 |

> **참고:**
> - VM 인스턴스에서 "HTTP 트래픽 허용"을 체크하면 80번 포트가 자동으로 열립니다.
> - "액세스 범위"를 "모든 Cloud API 전체 액세스 허용"으로 설정하면 Secret Manager 등 모든 GCP API를 사용할 수 있습니다.
> - 이미 생성된 인스턴스라면, 인스턴스 중지 → 수정 → 위 옵션들 체크/설정 후 저장하세요.

---

### 🌐 브라우저에서 접속 및 정상 동작 확인
- **외부에서 서비스가 잘 배포됐는지 확인하려면:**
    - GCP VM의 **외부 IP 주소**를 확인합니다. (VM 인스턴스 목록에서 확인 가능)
    - 브라우저 주소창에 아래와 같이 입력:
        - **80번 포트로 매핑한 경우:**
            - `http://<GCP_외부_IP>`
        - **8080 등 다른 포트로 매핑한 경우:**
            - `http://<GCP_외부_IP>:8080`
    - 정상적으로 서비스 화면이 뜨면 배포 성공!
- **Tip:**
    - curl 등으로도 빠르게 응답 상태를 확인할 수 있습니다.
    - 방화벽에 포트가 열려 있지 않으면 접속이 안 되니 꼭 확인하세요.

---

## 최종 실전 체크리스트

**1. Spring Boot 포트 확인**: 내 `application.properties` (또는 활성화할 프로필)의 `server.port`가   몇 번인지 확인! <br>
**2. 컨테이너 실행**: `docker run -d -p <쓸 포트>:<Spring Boot 포트>` 형식에 맞게 실행!  <br>
**3. 방화벽 확인**: GCP 방화벽에서 `<쓸 포트>`를 열었는지 확인!  <br>
**4. 브라우저 접속**: `http://<GCP 외부 IP>:<쓸 포트>`로 접속! (쓸 포트가 80이면 포트 번호 생략 가능)   <br>

## 📦 부록: 유용한 Docker 명령 요약

| 명령 | 설명 |
| --- | --- |
| `docker ps -a` | 모든 컨테이너(실행 중 + 중지) 조회 |
| `docker ps` | 실행 중인 컨테이너만 조회 |
| `docker logs <컨테이너ID>` | 컨테이너 로그 보기 |
| `docker stop <컨테이너ID>` | 컨테이너 중지 |
| `docker rm <컨테이너ID>` | 컨테이너 삭제 |
| `docker exec -it <컨테이너ID> bash` | 컨테이너 내부 bash 쉘 접속 |
| `docker images` | 로컬에 저장된 이미지 목록 조회 |
| `docker rmi <이미지ID>` | 이미지 삭제 |
| `docker pull <이미지명>` | 이미지 다운로드(풀) |
| `docker run -d -p <호스트포트>:<컨테이너포트> <이미지명>` | 컨테이너 실행(백그라운드) |

## 참고 문서

- [Google GCP 공식 문서](https://cloud.google.com/docs)
- [GoogleCloudPlatform_spring-cloud-gcp 깃허브](https://github.com/GoogleCloudPlatform/spring-cloud-gcp?utm_source=chatgpt.com)
- [Google Cloud 무료 프로그램](https://cloud.google.com/free/docs/free-cloud-features?hl=ko#compute)
<br>

- [Spring Cloud GCP 공식 문서](https://spring.io/projects/spring-cloud-gcp?utm_source=chatgpt.com)
- [Spring Cloud GCP 3.x Reference](https://googlecloudplatform.github.io/spring-cloud-gcp/reference/html/?utm_source=chatgpt.com)
- [SpringBoot Docker 사용 가이드](https://spring.io/guides/gs/spring-boot-docker)
- [SpringBoot에서 시크릿 매니저 사용 가이드](https://codelabs.developers.google.com/codelabs/cloud-spring-cloud-gcp-secret-manager?hl=ko#6)
<br>

- [Debian 서버에 Docker엔진 설치 가이드]https://docs.docker.com/engine/install/debian/)
- [GCP Secret Manager 정리본] ()
- [Linux_Docker_Vim 명령어 정리본] ()
- [Git 명령어 정리본] ()