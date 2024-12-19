### Git Squash 방법

Git에서 **squash**는 여러 커밋을 하나로 합쳐서 히스토리를 깔끔하게 만드는 데 사용주로 
`git rebase` 명령과 함께 사용함 

------

### **1️⃣ squash가 필요한 상황**

- 여러 번의 커밋으로 작업했지만, 이를 하나의 커밋으로 정리하고 싶을 때
- 불필요한 커밋(예: 디버그 메시지, 오타 수정 등)을 정리하고 싶을 때
- Pull Request를 깔끔하게 만들고 싶을 때

------

### **2️⃣ squash의 기본 명령**

1. **Rebase를 시작**

   ```
   git rebase -i HEAD~<숫자>
   ```

   - `<숫자>`는 squash하고 싶은 커밋 개수

   - 예: 마지막 3개의 커밋을 합치고 싶다면

     ```
     git rebase -i HEAD~3
     ```

2. **Rebase 편집 화면에서 squash 설정**

   - 명령을 실행하면 편집기가 열리고, 최근 커밋 리스트가 표시됨

     ```
     pick abc123 First commit
     pick def456 Second commit
     pick ghi789 Third commit
     ```

   - 여기서 

     첫 번째 커밋은 그대로 `pick`으로 유지

     하고, 나머지를 

     ```
     squash
     ```

     로 변경:

     ```
     pick abc123 First commit
     squash def456 Second commit
     squash ghi789 Third commit
     ```

3. **커밋 메시지 편집**

   - squash를 설정하고 저장하면, 커밋 메시지를 합치는 화면이 나타남

     ```
     This is a combination of 3 commits.
     # The first commit's message is:
     First commit
     
     # The following commit messages will also be included:
     Second commit
     Third commit
     ```

   - 원하는 커밋 메시지만 남기고 저장:

     ```
     First commit (with Second commit and Third commit)
     ```

4. **Rebase 완료**

   - 편집을 마치고 저장하면 squash가 완료됨

   - 충돌이 발생하면 충돌 파일을 수정한 뒤 아래 명령으로 진행

     ```
     git rebase --continue
     ```

------

### **3️⃣ squash된 결과 확인**

- `git log` 명령으로 결과를 확인
- 최근 커밋들이 하나로 합쳐져 있는 것을 확인할 수 있음

------

### **4️⃣ squash된 커밋 푸시**

- squash 후 원격 저장소에 푸시할 때는 강제로 푸시해야 함

  ```
  git push --force
  ```

------

### 

- **자동 Squash:** Pull Request를 GitHub에서 병합할 때, `Squash and merge` 버튼을 사용하면 자동으로 squash됨
- 주요 명령 요약
  - `git rebase -i HEAD~<숫자>`: 인터랙티브 리베이스 시작
  - `pick → squash`: 커밋 합치기
  - `git rebase --continue`: 충돌 해결 후 진행
  - `git push --force`: 변경 사항 원격 푸시