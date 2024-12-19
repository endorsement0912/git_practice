### 깃허브 관련 게임 : https://learngitbranching.js.org/?locale=ko

## 1️⃣ Git 자주 사용하는 명령어 
| 명령어                | 설명                                 | 
|-----------------------|------------------------------------|
| `git init`           | 새로운 깃 저장소 초기화              |
| `git status`         | 현재 작업 디렉토리 상태 확인          |
| `git add .`          | 모든 변경 파일을 스테이징에 추가       |
| `git add -u`         | 수정되거나 삭제된 기존 파일들을 스테이징      |
| `git commit -m "메시지"` | 변경사항 커밋                       |
| `git branch`         | 브랜치 목록 확인 및 생성             |
| `git checkout 브랜치명` | 특정 브랜치로 이동                  |
| `git switch 브랜치명`         | 다른 브랜치로 이동           |
| `git switch -c 브랜치명`        | 새로운 브랜치 생성 및 이동하기           |
| `git restore 파일명` | 마지막 커밋 기준으로 발생한 변경사항 되돌리기    |
| `git merge 브랜치명`  | 브랜치 병합                         |
| `git pull`           | 리모트 저장소에서 변경사항 가져오기    |
| `git push`           | 로컬 변경사항을 리모트 저장소로 푸시   |
| `git clone URL`      | 리모트 저장소 복제                   |
| `git log`            | 커밋 로그 확인                      |
| `git log --graph --oneline`   | 커밋 히스토리를 트리 형식으로 간략하게 표시    |
| `git blame 파일명`   | 파일에서 각 줄의 마지막 수정자 확인    |
| `git remote remove origin`   | 기존 원격 저장소 연결 제거    |

### + 추가 설명
* `git init` ➡️ 처음 깃 저장소를 설정할때 필요</br>
* `git blame` ➡️ 특정 파일의 각 줄에 대해 마지막으로 변경한 사람이 누구인지, 언제 수정되었는지를 확인</br>


## 2️⃣ Git 설정 명령어
| 명령어                | 설명                                 | 
|-----------------------|------------------------------------|
| `git config user.email`  | 현재 리포지터리의 사용자 이메일 확인          |
| `git config user.email 이메일주소`  | 현재 리포지터리의 사용자 이메일 설정         |
| `git config user.name`     | 현재 리포지터리의 사용자 이름 확인       |
| `git config user.name 유저닉네임`     | 현재 리포지터리의 사용자 이름 설정       |
| `git config --gloval alias.줄인명령어 "기존명령어"`     | git 명령어 줄이기       |
| `git config --global core.editor "code --wait"`     | VS Code를 git의 기본 편집기로 설정       |

### + 추가 설명
* `git config user.email/name (이메일주소 / 유저닉네임)` ➡️ 회사 계정과 개인 계정을 구분할때 좋음


## 3️⃣ Git 기본 명령어
| 명령어                | 설명                                 | 
|-----------------------|------------------------------------|
| `git init`  | git 리포지터리 생성          |
| `git add 파일명`  | 스테이징 영역에 추가         |
| `git add .`     | 모든 파일을 스테이징 영역에 추가       |
| `git commit -m "메세지"`     | 변경 사항 커밋       |
| `git status`     | 현재 상태 확인      |
| `git log"`     | 커밋 로그 확인       |
| `git log --oneline"`     | 커밋 로그를 한 줄로 확인        |
| `git branch"`     | 현재 로컬에 생성한 브랜치 확인     |
| `git branch 브랜치명"`     | 브랜치 생성     |
| `git branch -d 브랜치명"`     | 브랜치 삭제      |
| `git branch -D 브랜치명"`     | 브랜치 강제로 삭제   |
| `git branch -m 변경할_브랜치명"`     | 브랜치 이름 변경       |
| `git switch 브랜치명"`     | 브랜치 전환       |
| `git switch -"`     | 이전 브랜치로 돌아가기       |
| `git switch -c 브랜치명"`     | 브랜치를 생성하고 해당 브랜치로 전환      |
| `git merge 브랜치명"`     | 브랜치 병합       |
| `git clone URL주소"`     | 원격 리포지터리 복제       |
| `git push origin 로컬_브랜치명  | 브랜치를 원격 리포지터리로 푸시       |
| `git pull origin 로컬_브랜치명  | 원격 리포지터리에 있는 브랜치를 로컬로 가져와 병합       |


## 4️⃣ Git 응용 명령어
| 명령어                | 설명                                 | 
|-----------------------|------------------------------------|
| `git stash`  | 작업중인 변경사항을 임시 저장         |
| `git stash push -m "메세지"`  | 작업중인 변경 사항을 메시지와 함께 임시 저장         |
| `git stash list`     | 임시 저장한 변경 사항 확인       |
| `git stash apply "stash@{n}"`     | 심시 저장한 변경 사항 가져오기 (n은 숫자)       |
| `git stash pop "stash@{n}"`     | 임시 저장한 변경 사항을 가져오고 목록에서 삭제 (n은 숫자)  |
| `git commit --amend -m "메세지"`     | 최신 커밋을 덮어씌우고 수정       |
| `git commit --amend --no-edit`     | 메시지를 변경하지 않고 최신 커밋을 덮어씌우고 수정        |
| `git cherry-pick 커밋_해시값"`     | 특정 커밋을 현재 브랜치로 가져오기    |
| `git reset HEAD~n"`     | 특정 커밋으로 되돌리기(n은 숫자/삭제된 커밋의 작업 내용은 작업 디렉터리에 남아있음)      |
| `git rest --hard HEAD~n"`     | 특정 커밋으로 완전히 되돌리기(n은 숫자)       |
| `git revert HEAD~n"`     | 특정 커밋을 취소(n은 숫자)    |
| `git rebase 기준_브랜치"`     | 브랜치를 재배치 하기       |
| `git rebase -i HEAD~n"`     | git 히스토리 편집(n은 숫자)        |
| `git reflog"`     | git에 등록된 모든 기록 확인      |

### + 추가 설명
* `git stash` ➡️ A 브랜치에서 작업하던 도중 B 브랜치를 확인하기 위해 현재 작업 사항을 잠시 보관하고 싶을때 좋음</br>

* `git commit --amend -m "메세지"` ➡️ 방금 커밋한 커밋 메시지를 잘못 작성했을 때 유용</br>

* `git commit --amend --no-edit` ➡️ 작업한 내용이 방금 커밋한 메시지의 기능에 해당할 경우 메시지를 변경하지 않고 작업한 내용을 방금 커밋에 합치고 싶을 때 유용</br>

* `git cherry-pick 커밋_해시값"` ➡️ A 브랜치에서 작업한 특정 커밋이 B 브랜치에 포함되는 게 적합하다고 판단 했을 때 유용하며, C 브랜치에 포함된 작업 내용이 너무 많아서 D,E로 나눠야 하는 상황에서 D,E에 맞춰 커밋들을 분리할때 좋음</br>

* `git rebase 기준_브랜치"` ➡️ 현재 브랜치가 깃허브에 푸시되지 않은 상태에서 git 히스토리를 깔끔하게 정리하고 싶을 때 좋음(병합할 경우에는 병합 커밋이 생기므로)</br>

* `git rebase -i HEAD~n"`을 실행하면 커밋들을 편집할 수 있는 편집기가 열림</br>
    * pick : 커밋 유지</br>
    * reword : 커밋 메세지 변경</br>
    * fixup : 이전 커밋과 병합 후 해당 커밋 삭제</br>
    * squash : fixup과 reword를 합친 명령어</br>
    * drop : 커밋 삭제</br>
    * edit : rebase 도중 지정한 커밋 수정</br>

* `git reflog"` ➡️ 더 이상 불필요한 커밋이라 삭제했는데 다시 필요해져서 복구 하고 싶을 때 좋음</br>

