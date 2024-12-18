# 📓 깃 명령어 정리


| 명령어                | 설명                                 | 
|-----------------------|------------------------------------|
| `git init`           | 새로운 깃 저장소 초기화              |
| `git status`         | 현재 작업 디렉토리 상태 확인          |
| `git add .`          | 모든 변경 파일을 스테이징에 추가       |
| `git commit -m "메시지"` | 변경사항 커밋                       |
| `git branch`         | 브랜치 목록 확인 및 생성             |
| `git checkout 브랜치명` | 특정 브랜치로 이동                  |
| `git merge 브랜치명`  | 브랜치 병합                         |
| `git pull`           | 리모트 저장소에서 변경사항 가져오기    |
| `git push`           | 로컬 변경사항을 리모트 저장소로 푸시   |
| `git clone URL`      | 리모트 저장소 복제                   |
| `git log`            | 커밋 로그 확인                      |
| `git blame 파일명`   | 파일에서 각 줄의 마지막 수정자 확인    |

> 원격저장소 가져오는 방법

`git clone 레포지토리주소`   내 로컬 저장소 git 환경 초기화

`git init`   내 파일 변경사항 모두 저장

`git add`   변경사항을 이력에 남기기

`git commit -m "커밋메세지"`   커밋 메시지는 필수로 써줘야함

`git branch 브랜치명 git checkout 브랜치명`   브랜치 만들고 해당 브랜치로 작업환경(Working tree) 옮기기

`git remote add origin 레포지토리주소` 원격 저장소 등록하기 - origin이라는 이름으로 원격 레포지토리 주소가 등록됨

`git push -u origin 브랜치명`   한번만 원격저장소와 연동해주면 그 뒤로는 git push만 해주면 됨
