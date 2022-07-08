## Mac (os 터미널) 에서 SSH key 등록하기

1. ssh key 생성
   - 생성 파일의 경로 :  ~/.ssh/id_rsa
   - `ssh-keygen -t rsa -C GibHub 계정 이메일 주소`

2. GitHub Settings 메뉴 이동
   - New SSH Key 버튼 클릭
   - SSH Key 입력 : `cat ~/.ssh/id_rsa.pub`
 
3. 생성 완료 후 Generate 확인
   - `ssh -T git@github.com`
 
4. 맥에서 숨은 파일 확인하기 
   - shift + command + .

5. Git에서 기본 편집기 변경하기
  - `git config --global core.editor "notepad++"`
<br>

## git 최초 설정

1. Git 전역으로 사용자 이름과 이메일 주소를 설정
  - `git config --global user.name `본인이름`
  - `git config --global user.email 본인 이메일`

2. 설장한 내용 확인
  - `git config --global user.name`
  - `git config --global user.email`

3. 기본 브랜치명 main 으로 변경
  - `git config -global init.defaultBranch main`
<br>

## git 버전 만들기

1. 저장소에서 명령어 실행
  - `git init`

2. 새로운 디렉토리(저장소)를 만들고 초기화하는 과정을 한꺼번에 처리
  - `git init 디렉토리명`

3. 저장소 상태 확인
  - `git status`

4. 깃에서 스테이지에 올릴때 사용하는 명령어(스테이징)
  - `git add 파일명`

5. 현재저장소에서 수정된 파일을 한꺼번에 스테이지에 올리기
  - `git add .`

6. 스테이지에 올라온 파일 커밋메세지와 함께 커밋하기
  - `git commit -m "커밋메세지"`  

7. 저장소에 저장된 버전 확인	
  - `git log`

8. 스테이징과 커밋 한꺼번에 처리하기 ★새로 추가된파일이 없을때 한정
  - `git commit -am "커밋메세지"`

9. 저장할것과 저장하지 않을것을 지정
  - `git stash --patch`
<br>

## 커밋 내용 확인하기 

1. 작업트리에 있는 파일과 스테이지에 있는 파일을 비교
  - `git diff`
  - 스테이지에 있는 파일과 저장소에 있는 최신커밋을 비교해서 
  - 수정한 파일을 커밋하기전에 최종적으로 검토할수 있다
  - j : 위로 스크롤 
  - k : 아래로 스크롤, 
  - q : 종료

2. 커밋과 관련된 파일까지 함께 살펴보기
  - `git log --stat`

3. 파일 수정후 git status로 파일상태 확인하면
  - `Changes not staged for commit` 
  - modified : [수정된파일] 
  - 수정한파일이 스테이지에 올라가지 않았다고 알려준다

4. 한줄에 헌커밋씩 로그 확인
  - `git log --oneline`

5. 각 브렌치의 커밋을 함께 보기
  - `git log --oneline --branches`

6. 브렌치와 커밋의 관계를 그래프 형태로 표시
  - `git log --oneline --branches --graph`

7. 브렌치 비교
  - `git log 비교할대상브렌치 작업대상브렌치`

8. git add 파일명
  - `Changes to be committed` 
  - 커밋직전단계, 즉 staged 상태

9. 커밋한 내용 수정하기
  - `git commit --amend`
<br>

## 버전관리에서 제외하기

1. gitignore 설정
  - `vi .gitignore`
  - https://git-scm.com/docs/gitignore 참조
  - 모든 file.c : file.c
  - 최상위 폴더의 file.c : /file.c
  - 모든 .c 확장자 파일 : *.c
  - .c 확장자지만 무시하지 않을 파일 : !not_ignore_this.c
  - logs란 이름의 파일 또는 폴더와 그 내용들 : logs
  - logs란 이름의 폴더와 그 내용들 : logs/
  - logs 폴더 바로 안의 debug.log와 .c 파일들 : logs/debug.log, logs/*.c
  - logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log, logs/**/debug.log
<br>

## 작업 되돌리기

1. 작업 트리의 변경사항 취소
  - `git checkout -- 파일명`

2. 스테이지에서 내리기
  - HEAD 다음에 파일 이름을 지정하지 않으면 스테이지 모든 파일을 되돌린다
  - Unstaged changes after reset: // 파일이 스테이지에서 내려졌다는 메세지
  - Changes not staged for commit // 스테이지에서 내려감
  - git reset HEAD 파일명

3. 최신커밋 되돌리기
   - `git reset HEAD^`
   - Unstaged changes after reset: // 커밋이 취소되고 스테이지에서도 내려졌다는 메세지

4. 최근 커밋을 하기전 상태로  작업 트리를 되돌린다
   - `git reset --soft HEAD^`

5. 최근 커밋과 스테이징을 하기전 상태로 작업트리를 되돌린다(기본옵션)
   - `git reset --mixed HEAD^`

6. 최근 커밋과 스테이징, 파일 수정을 하기전 상태로 작업 트리를 되돌린다(복구불가)
   - `git reset --hard HEAD^`

7. 특정커밋으로 되돌리기(이후 버전은 삭제됨)
   - `git reset --hard 되돌리기하려는 특정커밋해시`

8. 커밋 삭제하지 않고 되돌리기 (취소한 커밋을 남겨둘때 사용)
  - `git revert 취소할마지막커밋해시`

9. HEAD는 여러 브렌치중에서 현재 작업중인 브렌치를 가르킨다
  - HEAD가 가리키고 있는 브렌치의 최신커밋을 원하는 커밋으로 지정
  - 즉 특정 커밋 되돌아가기
  - `git reset 되돌릴커밋해시`

10. 수정중인 파일 감추기
   - `git stash`
   - `git stash save`

11. 감춘파일 되돌리기
   - `git stash pop`

12.  stash 목록에서 최근항목을 되돌리지만 저장했던 내용은 그대로
   - `git stash apply`

13. revert는 reset 으로 다시 돌아갈 수 있다
   - `git revert`

14. conflicts 발생할 경우
   - hint: "git add/rm <pathspec>", then run
   - hint: "git revert --continue".
   - hint: You can instead ship this commit whit "git revert --skip".
   - hint: To abort and get back to the state before "git revert",
   - hint: run "git revert --abort".
   - 충돌나는 경우 파일을 삭제하거나 추가
   - 그리고 git revert --continue 로 진행 
   - commit 하지않고 revert하기 : `git revert --no-commit [커밋해시]`
   - 아직 커밋하지 않은 revert한 내용 취소 : `git reset --hard`
<br>

## Git Branch
1. 브렌치 확인
  - `git branch`

2. 브렌치 생성
  - `git branch 브렌치명`

3. 브렌치 이동 (checkout 명령어가 Git 2.23 버전부터 switch, restore 로 분리)
  - `git switch 브렌치명`

4. 브렌치 생성과 동시에 이동하기
  - `git switch -c 브렌치명`
  - 기존명령어 : `git checkout -b 브렌치명`

5. 브렌치 병합
  - `git merge 병합할대상브렌치`

6. 브렌치 병합 : 편집기창이 열리지않게/열리게
  - `git merge 병합할대상브렌치 --no--edit`
  - `git merge 병합할대상브렌치 --edit`

7. 브렌치 삭제(완전히 저장소에서 없애는게 아니라 흐름속에서 감추는것)
  - `git branch -d `브렌치명`
  - ★ 다른 브렌치로 적용되지 않은 내용의 커밋이 있을경우에는 -D 옵션으로 강제 삭제

8. 브렌치 이름 바꾸기
  - `git branch -m 기존브렌치명 새브렌치명`
<br>

## 원격 저장소 연결
 
1. 원격 저장소 연결하기
  - `git remote add origin 저장소주소`

2. github 권장 -기본 브렌치명 main으로 
  - `git branch-M main`

3. 원격 저장소 연결되었는지 확인하기
  - `git remote`
  - `git remote -v`

4. 원격 저장소에 푸시하기
  - push에 -u 옵션을 붙이면 다음부터 
  - git push 명령어만으로 원격저장소 branch에 커밋 가능
  - -u 또는 --set-upstream : 현재 브렌치와 명시된 원격 브랜치 기본 연결
  - `git push -u origin main`
  - `git push -u origin master`

5. 원격자종소에서 파일 가져오기
  - `git pull origin main`
  - `git pull origin master`
  - `git pull origin main --allow-unrelated-histories`

6. 원격 지우기(로컬 프로젝트와의 연결만 없애는것, GitHub의 레포지토리는 지워지지 않음)
  - `git remote remove origin원격이름`
<br>

## 충돌 해결하기 (Revase vs Merge)

1. rebase 로 충돌 코드 수정
  - `git rebase 합칠브렌치명`

2. 충돌 해결 후 rebase 진행하기 
  - `git rebase --continue`

3. vim 에서 commit message 확인 후
  - wq 종료 

4. 만약 rebase 로 충돌 코드 수정이 어려울 경우
  - `git rebase --abort`
  - ★ 두마디짜리 브렌치를 rebase 했는데 결과에는 왜 한마디만 추가되는지?
  - 충돌 해결 중 두번째 것에서는 curreunt, 즉 main 브렌치것을 채탯했기때문에, 
  - 즉 rebase가 의미가 없어졌으므로 커밋으로 추가할 필요가 없어졌기 때문   
<br>
## 병합하기 

1. merge로 충돌 코드 수정 
  - `git merge 합칠 브렌치명`

2. 에드 후 커밋
  - `git add .`
  - `git commit`
  - vim 에서 conflit message 확인후 :wq 종료

3. merge 중단하기
  - `git merge --abort`
<br>
😄😄😄
