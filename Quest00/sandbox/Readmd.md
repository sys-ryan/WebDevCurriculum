# Quest.00 형상관리 시스템

## Checklist

- ### 형상관리 시스템은 왜 나오게 되었을까요?

  형상관리 시스템은 소프트웨어의 변경 사항을 `체계적으로 추적하고 통제`하기 위해 나왔습니다.
  체계적으로 추적하고 통제한다는 것은, 어떤 문서나 파일이 변경되었을 경우 변경된 내역을 기록하였다가 나중에 찾아보아야할 경우에 `변경 원인`과 `변경 사항`을 확인해야 할 경우 대한 관리를 의미합니다.

- ### git은 어떤 형상관리 시스템이고 어떤 특징을 가지고 있을까요? 분산형 형상관리 시스템이란 무엇일까요?

  git은 software development 를 위해 사용되는 분산형 형상관리 시스템(DVCS) 입니다.
  분산형 형상관리 시스템은 모든 파일, 브랜치, 프로젝트에 대한 모든 접근을 `독립적인 환경`에서 접근할 수 있도록 해주는 형상관리 시스템입니다.
  중앙집중화된 VCS와는 다르게, 중앙 repository에 지속적으로 연결되어있을 필요가 없고, 개발자가 시간과 장소에 상관없이 비동기적으로 개발에 협업할 수 있습니다.

- ### git은 어떻게 개발되게 되었을까요? git이 분산형 시스템을 채택한 이유는 무엇일까요?

  리누스 토발즈가 리눅스를 개발한 이후, `BitKeeper`라는 툴로 리눅스의 버전을 관리했었습니다.
  이후 BitKeeper와 리눅스 커뮤니티의 마찰(내부 동작 원리 분석 시도)로 BitKeeper가 유료화 되었고, 이에 리누스 토발즈가 BitKeeper를 대신할 버전 관리 시스템으로 만들어진 것이 git 입니다.

  git은 다음과 같은 목표를 가지고 설계 및 개발되었습니다.

  1. 빠른 속도
  2. 단순한 디자인
  3. 비선형적 개발 지원(많은 수의 브랜치를 병행)
  4. 완전 분산형 시스템
  5. 리눅스와 같은 거대한 프로젝트도 속도저하의 문제 없이 관리할 수 있는 시스템

- ### git과 GitHub은 어떻게 다를까요?

  git : 소프트웨어의 변경사항을 추적하고 통제하기 위한 `분산 버전 관리 시스템`
  github : 분산 버전 관리 시스템인 git을 사용하는 프로젝트를 지원하는 `웹호스팅 서비스`

- ### git의 clone/add/commit/push/pull/branch/stash 명령은 무엇이며 어떨 때 이용하나요? 그리고 어떻게 사용하나요?

  - `git clone`
    원격에 존재하는 repository의 local copy를 생성
    프로젝트의 파일, 히스토리, 브랜치를 모두 포함
    사용 방법 :

  ```
  git clone <url>
  ```

  - `git add`
    변경 사항을 statge.
    git은 개발자의 codebase에 대한 `변경 사항을 추적`하는데, 이 변경 사항을 프로젝트의 히스토리에 포함시키기 위해서는 변경 사항을 `stage`하고 해당 변경 사항에 대한 `snapshot`을 생성해야 함.
    사용 방법 :

  ```
  git add <파일 이름>
  ```

  - `git commit`
    snapshot을 프로젝트 히스토리에 추가하고,변경사항 추적 프로세스를 마침.
    git add로 stage된 모든 것들이 snapshot에 포함됨
    사용 방법 :

  ```
  git commit
  git commit -m "이번 snapshot에 대한 설명"
  ```

  - `git push`
    branch 에 반영된 local commit들을 원격 repository에 업데이트
    사용 방법 :

  ```
  git push origin <branch name>
  ```

  만약 기존에 있던 원격 저장소를 복제한것이 아니라면, 먼저 원격 서버의 주소를 git에게 알려줘야 함

  ```
  git remote add origin <remote repository address>
  ```

  - `git pull`
    local 개발 내역들을 remote 개발 내역으로 업데이트.
    팀 구성원이 remote branch에 commit을 했고, 그 변경 사항들(commit 내용들)을 local invironment에 반영하고 싶을 때 이 명령어를 사용

          로컬 저장소를 원격 저장소에 맞춰 갱신

    원격 저장소의 변경 내용이 로컬 작업 디렉토리에 받아지고(fetch), 병합(merge) 됨
    사용 방법 :

  ```
  git pull
  ```

  다른 branch에 있는 변경 내용을 현재 branch에 병합하려면 다음 명령을 실행

  ```
  git merge <branch name>
  ```

  변경 내용을 병합하기 전에, 어떻게 바뀌었는지 비교 가능

  ```
  git diff <original branch> <counterpart branch>
  ```

  - `git branch`
    local repository에서 작업한 branch들을 보여줌
    사용 방법 :

  ```
  git branch

  git branch -d <branch name> // delete branch
  ```

  - `git stash`
    A branch에서 작업을 완료 후 B branch 를 따서 작업 중에, 다시 A branch로 돌아가서 수정할 상황이 생겼을 때, B branch의 현재 상태를 잠시 저장 후 다시 돌아올 수 있도록 함
    사용 방법 :

  ```
  git commit
  git stach

  git stash list

  git stach apply `stash ID`
  git stash drop `stash ID` // stash list 내역 지우기

  git stash pop // git stash 상태로 돌아가고, LIST에서 바로 삭제하기
  ```
