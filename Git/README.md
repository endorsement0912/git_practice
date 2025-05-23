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

1. `git clone 레포지토리주소` ➡️ 내 로컬 저장소 git 환경 초기화(본인꺼)

2. `git init` ➡️ 내 파일 변경사항 모두 저장(본인꺼)

3. `git add . ` ➡️ 변경사항을 이력에 남기기(본인꺼)

4. `git commit -m "커밋메세지"` ➡️ 커밋 메시지는 필수로 써줘야함(본인꺼)

5. `git branch 브랜치명 git checkout 브랜치명` ➡️ 브랜치 만들고 해당 브랜치로 작업환경(Working tree) 옮기기(본인꺼)

6. `git remote add origin 레포지토리주소` ➡️ 원격 저장소 등록하기 : origin이라는 이름으로 원격 레포지토리 주소가 등록됨(타인꺼)

7. `git push -u origin 브랜치명` ➡️ 한번만 원격저장소와 연동해주면 그 뒤로는 git push만 해주면 됨(타인꺼)
  
<br>

## 📤 로컬저장소에서 GitHub에 업로드 하는 방법
  
1. `git add .` ➡️ 변경 사항을 추가

2. `git commit -m "커밋메세지"`  ➡️ 변경 사항을 커밋하여 저장소에 기록

3. `git status(선택적)` ➡️ 변경 사항이 잘 반영 되었는지 확인

4. `git push (origin main)` ➡️ 로컬 커밋을 원격 저장소에 업로드
<br>

## 🗂️ 리포지토리 변경 및 원격 저장소 설정 방법
⛓️‍💥 새 리포지토리로 변경하기
 1. `git remote remove origin` ➡️ 기존 원격 저장소 연결을 제거
 2. `git clone 레포지토리주소` ➡️ 새 리포지토리를 로컬에 클론
<br>

🔗 기존 리포지토리로 변경하기
 1. `git remote remove origin` ➡️ 기존 원격 저장소 연결을 제거
 2. `git remote add origin 레포지토리주소` ➡️ 자신의 기존 원격 저장소를 추가

    * `git clone 레포지토리주소`는 이미 클론된 리포지토리 디렉토리가 있는 경우에는 사용불가
    * 기존 작업 디렉토리에서 바로 변경하고 싶으면 `git remote add origin 레포지토리주소`가 더 적합

 3. `git push -u origin 브랜치명` ➡️ 로컬 브랜치의 커밋을 원격 저장소에 푸시
<br>

## 🔗 main_branch 기반으로 branch 생성 방법

1. 저장소 클론 또는 이동
`git clone [repo_url]`
`cd [repo_name]`

2. 최신 main 브랜치 받기
`git checkout main`
`git pull origin main`

3. 새 브랜치 생성 및 이동
`git checkout -b 새_브랜치_이름`

4. 원격 저장소에 브랜치 푸시
`git push origin 새_브랜치_이름`

<br>

## ⬅️ Pull Requests 방법
📍참고 : https://blog.naver.com/endorsement_r/223850161175
1. 깃허브 화면에서 pull requests 누르기

2. New Pull Requests 누르기

3. Base : 보낼곳 / compare : 보낼 내용

4. Create Pull request * 2 누르기

<br>



## 🔄 원본 레포지토리와 동기화하는 방법
1. `git remote add upstream 원본레포지토리주소` ➡️ 업스트립 추가(원본 레포지 토리와 연결) - `git remote -v` 명령어로 확인하면 upstream이 추가된 걸 볼 수 있음
   
2. `git fetch upstream` ➡️ 원본 저상소의 최신 코드 가져오기

3. `git checkout 브랜치명 (메인 브랜치로 이동)` ➡️ 내 브랜치와 병합
   `git merge upstream/브랜치명 (원본 저장소의 브랜치와 병합)`
    
4. `git push origin 브랜치명` ➡️ 변경 사항을 내 GitHub fork에 푸시
<br>

## ⬇️ 다른 레포지토리 import 방법
1. import 하고 싶은 레포지토리에서 Pull requests 클릭

2. 오른쪽 상단의 + 아이콘을 클릭

3. Import repository 클릭

4. Your source repository details에 복사하려는 repository의 git주소 입력(github repo에서 가지고 오는 경우 .git도 마지막에 붙음)

5. Your username for your source repository, Your access token or password for your source repository - 해당 레포지토리에 권한을 가진 유저 정보 입력하는 곳 (필수는 아님)

6. Your new repository details에 새로운 레포지토리 이름 입력하고, Begin Import를 클릭 
<br>

## 🗑️ 특정 branch 삭제 방법
1. `git checkout 다른_브랜치`     # 다른_브랜치로 먼저 이동
2. `git branch -d 삭제할_브랜치명` # 브랜치 삭제

  ➕ `git switch -c 브랜치명` # 새로운 브랜치 생성 및 이동하기
<br>

## 🗑️ 레포지토리 삭제 방법
1. 삭제할 레포지토리에서 상단의 Settings 클릭

2. 화면 맨 아래에 Danger Zone에서 Delete this repository를 클릭

3. I want tp delete this repository 클릭

4. I have read and understand these effects 클릭

3. Ti confirm, type "____레포지토리주소___"에서 []에 레포지토리 주소 그대로 적고 'Delete this repository' 버튼 클릭

4. password를 입력한 후 confirm 버튼 클릭

