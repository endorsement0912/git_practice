## 🔗 이름으로 된 레포지토리 생성후 자바스프링부트 업로드 하는 방법


1️⃣ 스프링부트 기본 프레임워크 다운 방법

>1. organiztion 홈에서 New Repository로 본인이름의 레포생성
>
>2. https://start.spring.io/ 로 접속후 옵션을 아래에 맞게 설정
>   * Project : Gradle - Groovy java 
>   * Laguage : java
>   * Project Metadata - GROUP : gitdemo
>   * Project Metadata - Artifact : 이름
>   * Project Metadata - Name : 이름
>   * Project Metadata - Packaging : Jar
>   * Project Metadata - Java : 21
>
>3. 하단에 Generation 누르면 zip이 저장됨 ➡️ 압축 해제

</br>

2️⃣ 레포지토리에 스프링 부트 기본 프레임워크 업로드 방법

>1. VS Code에서 File ➡️ Open Folder ➡️ 압축 해제된 폴더 선택
>
>2. 터미널 열어서 `git init` ➡️ git 저장소 초기화
>
>3. `git remote add origin 이름으로_생성한_레포_HTTP주소` ➡️ 원격 저장소 추가
>
>4. `git add .` ➡️ 변경 사항 커밋
>
>5. `git commit -m "커밋메세지"` ➡️ 커밋 메세지
>
>6. `git push -u origin main` ➡️ git에 푸시
    * 다른 브랜치명으로 푸시하고 싶으면 `git branch -M 브랜치명`을 한후에 `git push -u origin ` 

</br>
