# git & github(youtube)

Created: September 13, 2022
Review: No

## 강좌 정보

이름 : [깃 끝장내기] 제대로 파는 Git & GitHub 강좌

URL : [https://www.youtube.com/watch?v=1I3hMwQU6GU](https://www.youtube.com/watch?v=1I3hMwQU6GU)

## 설치

1. [sourcetree](https://www.sourcetreeapp.com/) → GUI tool로 전세계적으로 많이 사용함
2. [iterm2](https://iterm2.com/) → Upgrade mac terminal UI
3. [vscode](https://code.visualstudio.com/) terminal

## Git 설정 & 프로젝트 관리 시작하기

1. git 최초 설정
    
    나중에 협업을 위해 어떤 작업을 누가 했고, 어떻게 연락을 하는지 세팅
    

```bash
git config --global user.name "(name)"
git config --global user.email "(email)"
```

기본 브랜치명 변경(권유 master → main)

```bash
git config --global init.defaultBranch main
```

## Git에게 맡기지 않을 것들

1. 포함할 필요가 없을 때 → 빋르 결과물, 라이브러리
2. 포함하지 말아야 할 때 → 보안 이슈 파일 

**.gitignore 파일 생성**

[.gitignore 형식 보기](https://dkswnkk.tistory.com/575)

## Git init & commit

```bash
git add .
git add (file name)

git commit -m "message"
```

## git을 사용하여 과거로 돌아가는 방법

### Reset

시간을 과거로 돌리고 현재 흔적은 지움

![Untitled](git%20&%20github(youtube)%20674d0aa0cdbc46fabac61a3fba640c7b/Untitled.png)

```bash
git log # commit hash 확인
git reset --hard (돌아갈 커밋 해시)
```

git 파일을 백업해두고 과거 상태로 돌아가고 싶을때 → 파일들 복원됨

실제 프로젝트에서는 사용되지 않음

```bash
git reset --hard
```

### Revert

과거로 돌아간 흔적을 한단계 더 남김

한번 공유가 된 커밋들은 반드시 revert를 사용해야 함 → 충돌 발생함

![Untitled](git%20&%20github(youtube)%20674d0aa0cdbc46fabac61a3fba640c7b/Untitled%201.png)

```bash
git revert (돌아갈 커밋 해시)
git reset --hard (리셋할 커밋 해시)
```

- Revert 할 때, 그 이후 수정한 내역 때문에 충돌이 일어나는 경우에는
    1. `git rm (filename)` 로 Git에서 해당 파일 삭제
    2. `git revert —continue`
    3. `:wq` 커밋 메세지 저장
    

### 커밋하지 않고 revert 하기

revert와 다른 변경사항도 함께 커밋하기 위해 사용할 수 있음

1. `git revert —no-commit (hash)` 
2. 함께 커밋할 수정사항
3. 커밋 

## 여러 Branch 만들어보기

**브랜치가 필요할 때**

1. 프로젝트를 하나 이상의 모습으로 관리해야 할 때
2. 여러 작업들이 각각 독립되어 진행될 때

```bash
git branch (branch name)
git branch
git switch (created branch name)
git switch -c (branch name)
git branch -d (delete branch name)
git branch -m (modify branch name) (new branch name)
```

![Untitled](git%20&%20github(youtube)%20674d0aa0cdbc46fabac61a3fba640c7b/Untitled%202.png)

sourcetree로 확인하면 브랜치가 갈라지는 걸 볼 수 있음

## branch를 합치는 두가지 방법

1. **merge**
    
    합침
    

![Untitled](git%20&%20github(youtube)%20674d0aa0cdbc46fabac61a3fba640c7b/Untitled%203.png)

`git merge (병합할 branch name)`

merge는 하나의 커밋이기 때문에 돌아갈 수 있음

사용이 끝난 브랜치는 삭제해주면 됨

- **충돌이 발생하는 경우(서로 같은 파일을 수정했을때)**
    
    vscode같은 경우 충돌이 일어난 경우 선택 기능이 존재함
    
    선택후 add & commit을 해주고 똑같이 진행하면 됨
    
1. **rebase**
    
    branch 수정사항을 옮겨 붙임 → 곁가지를 옮겨 붙임으로서 내역들을 확인하기 쉬워짐
    
    rebase를 실행해도 main의 포인트는 옮겨지지 않음
    
    **순서**
    
    1. 합칠 브랜치로 `switch`
    2. `git rebase main`
    3. main 브랜치로 `switch`
    4. `git merge 합칠브랜치`
    5. 합쳐진 브랜치 삭제 `git branch -d (delete branch name)`

![Untitled](git%20&%20github(youtube)%20674d0aa0cdbc46fabac61a3fba640c7b/Untitled%204.png)

## github

**로컬 저장소의 커밋과 origin의 수정사항이 충돌할 때**

1. `git pull --no-rebase` → merge 방식
2. `git pull —rebase` → rebase 방식 
3. `git push`

**원격 저장소의 내용이 잘못되어 로컬 저장소의 소스로 강제로 맞출 때**

1. `git push —force`

**원격 브랜치 로컬에 받아오기**

github에서 브랜치 만들어진 경우 `git fetch` 로 변경사항 확인

`git switch -t origin/remote` 로 원격 브랜치로 변경

`git push origin —delete (원격 브랜치명)` → 원격 브랜치 삭제