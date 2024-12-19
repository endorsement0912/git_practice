## ☑️ Git 용어 정리
* Git : 버전 관리 시스템
* GitHub : Git으로 관리하는 프로젝트를 올려둘 수 있는 사이트
* CLI : 커맨드라인 인터페이스로 명령어를 하나씩 입력하는 방식
* Git Bash : CLI 방식으로 Git을 사용할 수 있는 환경
* commit : 버전 관리를 통해 생성된 파일, 혹은 그 행위
* log : 지금까지 만든 커밋을 모두 확인
* checkout : 원하는 지점으로 파일을 되돌릴 수 있음 = 타임머신 기능
* repository : 저장소를 의미
* push : 로컬 저장소의 커밋(버전 관리한 파일)을 원격 저장소에 올리는 것
* pull : 원격 저장소의 커밋을 로컬 저장소에 내려 받는 것
<br>

## 📥 Github에서 원격저장소 가져오는 방법(초기 설정)

1. `git clone 레포지토리주소` ➡️ 내 로컬 저장소 git 환경 초기화

2. `git init` ➡️ 내 파일 변경사항 모두 저장

3. `git add . ` ➡️ 변경사항을 이력에 남기기

4. `git commit -m "커밋메세지"` ➡️ 커밋 메시지는 필수로 써줘야함

5. `git branch 브랜치명 git checkout 브랜치명` ➡️ 브랜치 만들고 해당 브랜치로 작업환경(Working tree) 옮기기

6. `git remote add origin 레포지토리주소` ➡️ 원격 저장소 등록하기 : origin이라는 이름으로 원격 레포지토리 주소가 등록됨

7. `git push -u origin 브랜치명` ➡️ 한번만 원격저장소와 연동해주면 그 뒤로는 git push만 해주면 됨
  
<br>

## 📤 로컬저장소에서 GitHub에 업로드 하는 방법
  
1. `git add .` ➡️ 변경 사항을 추가

2. `git commit -m "커밋메세지"`  ➡️ 변경 사항을 커밋하여 저장소에 기록

3. `git status(선택적)` ➡️ 변경 사항이 잘 반영 되었는지 확인

4. `git push (origin main)` ➡️ 로컬 커밋을 원격 저장소에 업로드
<br>

## 🗂️ 리포지토리 변경 및 원격 저장소 설정 방법
⛓️‍💥 새 리포지토리로 변경하기
* `git remote remove origin` ➡️ 기존 원격 저장소 연결을 제거
* `git clone 레포지토리주소` ➡️ 새 리포지토리를 로컬에 클론

<br>

🔗 기존 리포지토리로 변경하기
* `git remote remove origin` ➡️ 기존 원격 저장소 연결을 제거
* `git remote add origin 레포지토리주소` ➡️ 자신의 기존 원격 저장소를 추가

    * `git clone 레포지토리주소`는 이미 클론된 리포지토리 디렉토리가 있는 경우에는 사용불가
    * 기존 작업 디렉토리에서 바로 변경하고 싶으면 `git remote add origin 레포지토리주소`가 더 적합

* git push -u origin 브랜치명 ➡️ 로컬 브랜치의 커밋을 원격 저장소에 푸시

<br>

## ⬅️ Pull Requests 방법
1. 깃허브 화면에서 pull requests 누르기

2. New Pull Requests 누르기

3. Base : 보낼곳 / compare : 보낼 내용

4. Create Pull request * 2 누르기
