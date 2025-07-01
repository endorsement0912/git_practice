# 🔐 GCP Secret Manager 연동 가이드 (Spring Boot)

## 1. GCP에서 Secret 생성

1. [GCP 콘솔 접속](https://console.cloud.google.com/)
2. 좌측 메뉴 → **Security** → **Secret Manager** 클릭
3. **Secret 만들기** 클릭
4. 이름, 값 입력 후 **만들기**
5. (필요시)IAM & 관리자에서 VM/서비스 계정에 Secret Manager 접근 권한(`Secret Manager Secret Accessor` 또는 `roles/secretmanager.secretAccessor`= 보안 비밀 관리자 관리) 부여
6. **(중요!) VM 인스턴스 생성 시 아래 옵션을 꼭 확인하세요:**
   - "액세스 범위: 모든 Cloud API 전체 액세스 허용" 선택 (Secret Manager 등 사용시)
   - 이미 생성된 인스턴스라면, 인스턴스 중지 → 수정 → 위 옵션들 체크/설정 후 저장

---

## 2. 서비스 계정 키 발급 및 VM/로컬에 적용

1. **IAM & 관리자 > 서비스 계정**에서 새 서비스 계정 생성 (또는 기존 계정 사용)
2. **키 > 키 추가 > 새 키 만들기 > JSON** 선택 후 다운로드
3. VM 또는 로컬에 업로드 (예: `/home/ubuntu/secret-key.json` 또는 `C:\경로\secret-key.json`)
4. 환경변수로 등록  
   - **리눅스/맥(Bash):**
     ```bash
     export GOOGLE_APPLICATION_CREDENTIALS="/home/ubuntu/secret-key.json"
     ```
     - (일시적 적용: 터미널 창에서만 유효)
     - **영구 적용하려면:**
       1. `sudo nano ~/.zshrc` (또는 `~/.bashrc`)
       2. 맨 아래에 위 `export ...` 한 줄 추가
       3. `Control + O` (저장), `Enter` (확정), `Control + X` (에디터 종료)
       4. `source ~/.zshrc` (변경 사항 적용)
   - **Windows CMD:**
     ```cmd
     set GOOGLE_APPLICATION_CREDENTIALS=C:\경로\secret-key.json
     ```
   - **Windows PowerShell:**
     ```powershell
     $env:GOOGLE_APPLICATION_CREDENTIALS="C:\경로\secret-key.json"
     ```
   (이 환경변수는 Spring Boot가 GCP API를 사용할 때 인증에 사용됨)

---

## 3. Spring Boot에서 Secret Manager 연동

### 1) 의존성 추가 (pom.xml)
```xml
<!-- 🔒 GCP Secret Manager 사용시 활성화 (최신 Spring Cloud GCP 6.x 기준) -->
<dependency>
  <groupId>com.google.cloud</groupId>
  <artifactId>spring-cloud-gcp-dependencies</artifactId>
  <version>6.2.2</version>
  <type>pom</type>
  <scope>import</scope>
</dependency>
```
```xml
<!-- 🔒 GCP Secret Manager -->
<dependency>
  <groupId>com.google.cloud</groupId>
  <artifactId>spring-cloud-gcp-starter-secretmanager</artifactId>
</dependency>
```

### 2) application.properties에 Secret Manager 연동 (최신 방식)
```properties
# Secret Manager의 값을 Spring Boot 환경 변수처럼 자동으로 불러오기
spring.config.import=sm://
```
- 이 설정을 추가하면, Secret Manager에 저장된 key/value가 Spring Boot의 환경 변수/프로퍼티로 자동 매핑됨.

#### 예시
- Secret Manager에 `my-secret`이라는 이름으로 값을 저장했다면,
- Spring Boot에서 `${my-secret}` 또는 `@Value("${my-secret}")`로 바로 사용 가능!

### (참고) 구버전 방식
- Spring Cloud GCP 4.x, 5.x에서는 아래처럼 직접 프로퍼티에 sm://로 참조함.
```properties
my.secret.value=sm://my-secret
```
- 이 방식은 `@Value("${my.secret.value}")`로 주입해서 사용함.

---

## 4. (선택) Secret 버전 지정
기본적으로 최신 버전을 사용하지만, 특정 버전을 쓰고 싶다면:
```properties
my.secret.value=sm://my-secret/versions/2
```

---

## 5. 로컬 개발 환경에서 사용하려면?
- 로컬에도 서비스 계정 키 파일을 두고,  
  `GOOGLE_APPLICATION_CREDENTIALS` 환경변수로 경로를 지정하면 동일하게 동작함.

---

## 6. 참고 공식문서
- [Spring Cloud GCP Secret Manager 공식 가이드](https://cloud.spring.io/spring-cloud-gcp/reference/html/index.html#secret-manager)
- [GCP Secret Manager 공식문서](https://cloud.google.com/secret-manager/docs)
- [Spring Boot를 사용하여 Secret Manager에서 사용자 인증 정보/보안 비밀 검색](https://codelabs.developers.google.com/codelabs/cloud-spring-cloud-gcp-secret-manager?hl=ko#0)