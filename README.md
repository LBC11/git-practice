## Git setting
#### git version 확인  

    git --version
    

#### 윈도우와 맥의 enter 차이로 인한 오류 방지
    git config --global core.autocrlf true 
    
## Git 최초 설정  
#### Git 전역으로 사용자 이름과 이메일 주소를 설정
    git config --global user.name "(본인 이름)"
    
    git config --global user.email "(본인 이메일)"
    
#### 확인 방법
    git config --global user.name
    
    git config --global user.email
    
#### 기본 브랜치명 변경
    git config --global init.defaultBranch main  
    
## 프로젝트 생성 & Git 관리 시작  
#### .git folder 생성
    git init
    
#### file 상태 확인하기
    git status
    
## Git의 관리에서 특정 파일/폴더를 배제해야 할 경우
+ 포함할 필요가 없을 때  
    + 자동으로 생성 또는 다운로드되는 파일들 (빌드 결과물, 라이브러리)  
+ 포함하지 말아야 할 때  
    + 보안상 민감한 정보를 담은 파일  

#### .gitignore 형식  
<pre>
<code>
# 이렇게 #를 사용해서 주석

# 모든 file.c
file.c

# 최상위 폴더의 file.c
/file.c

# 모든 .c 확장자 파일
*.c

# .c 확장자지만 무시하지 않을 파일
!not_ignore_this.c

# logs란 이름의 파일 또는 폴더와 그 내용들
logs

# logs란 이름의 폴더와 그 내용들
logs/

# logs 폴더 바로 안의 debug.log와 .c 파일들
logs/debug.log
logs/*.c

# logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log
logs/**/debug.log
</code>
</pre>

## 변화를 타임캡슐에 담아 묻기
#### 파일 하나 담기
    git add "(파일 이름)"
    
#### 모든 파일 담기
    git add .
    
#### 타임캡슐 묻기
    git commit 
    
#### VI 입력 모드
+ 입력 시작: i
+ 입력 종료: ESC
+ 저장 없이 종료: q
+ 저장 없이 강제 종료: q!
+ 저장하고 종료: wq
+ 위로 스크롤: k
+ 아래로 스크롤: j

#### commit message 함계 작성
    git commit -m "커밋 메시지"
    
#### commit 확인
    git log
    
## 과거로 돌아가는 2가지 방법
+ reset : 원하는 시점으로 돌아간 뒤 이후 내역들을 지웁니다.  
    git reset --hard (돌아갈 커밋 해시) 
    
+ revert : 되돌리기 원하는 시점의 커밋을 거꾸로 실행합니다.
    git revert (되돌릴 커밋 해시)
    
+  커밋해버리지 않고 revert하기
    git revert --no-commit (되돌릴  커밋 해시)
    
+ 참고
    + Git에서 reset, revert로 이동할 때 저장되어 있는 파일을 불러와서 현재의 파일에 변경을 주는 것이지 지금 현재의 파일을 통째로 저장되어 있는 파일로 바꾸는 것이 아니다.
    + => 현재의 파일 중 저장되어 있던 snapshot에 없던 file은 삭제되는 것이 아니라 그대로 남아있다.  
    
## 여러 branch 만들어 보기
#### branch 생성
    git branch "(branch 이름)"
    
#### branch 목록 확인
    git branch
    
#### branch 이동
    git switch "(branch 이름)"
    
#### branch 생성과 동시에 이동하기
    git switch -c "(branch 이름)"
    
#### branch 삭제하기
    git branch -d "(branch 이름)"
    
#### branch 강제 삭제하기(지워질 branch에만 내용이 있을 경우)
    git branch -D "(branch 이름)"
    
#### branch 이름 바꾸기
    git branch -m "(기존 branch 이름)" "(새로운 branch 이름)"
    
#### 여러 branch의 내역 보기
    git log --all --decorate --oneline --graph
    
## branch를 합치는 2가지 방법
+ merge : 두 브랜치를 한 커밋에 이어붙입니다.  
    + 브랜치 사용내역을 남길 필요가 있을 때 적합한 방식입니다.  
    + 다른 형태의 merge에 대해서도 이후 다루게 될 것입니다.  

+ rebase : 브랜치를 다른 브랜치에 이어붙입니다.  
    + 한 줄로 깔끔히 정리된 내역을 유지하기 원할 때 적합합니다.  
    + 이미 팀원과 공유된 커밋들에 대해서는 사용하지 않는 것이 좋습니다.  
    
#### merge
+ add-coach 브랜치를 main 브랜치로 merge
    + main 브랜치로 이동
    + 아래의 명령어로 병합
```
    git merge add-coach
```
+ merge는 reset으로 되돌리기 가능
    + merge도 하나의 커밋
    + merge하기 전 해당 브랜치의 마지막 시점으로

#### rebase
+ new-teams 브랜치를 main 브랜치로 rebase
    + new-teams 브랜치로 이동
    + merge때와는 반대!
    + 아래의 명령어로 병합
```
    git rebase main
```

## 충돌 해결하기
#### merge
+ 충돌 해결이 어려운 경우
```
    git merge --abort
```

+ 충돌 해결이 가능한 경우
    + 충돌 부분 수정
    + git add .
    + git commit

#### rebase
+ 충돌 해결이 어려운 경우
```
    git rebase -- abort
```
+ 충돌 해결이 가능한 경우
    + 충돌 부분 수정
    + 아래 명령어로 계속
```
    git rebase --continue
```
    + git add .
    + git commit
    
    

## 원격 저장소 사용
#### 원격 저장소 추가
    git remote add "(원격 저장소 이름)" "(원격 저장소 주소)"
    
#### 원격 기본 브랜치명 설정(main이 기본)
    git branch -M "(branch 이름)"
    
#### 로컬 저장소의 커밋 내용들 원격으로 push
    git push -u "(원격 저장소 이름)" "(branch 이름)"
    
+ -u 또는 --set-upstream: 현재 브랜치와 명시된 원격 브랜치 기본 연결

#### 원격 목록 보기
    git remote
    
    #자세히 보기
    git remote -v
    
#### 원격 지우기(로컬 프로젝트와의 연결만 없애는 것. Github의 레포지토리는 없어지지 않음
    git remote remove "(원격 저장소 이름)"
    
#### 원격 저장소의 project 복사
    git clone "(원격 저장소 주소)"


## push와 pull
#### push
    # 앞에서 -u로 설정해놓았을 경우 
    git push
    # 안 해놓은 경우
    git push "(원격 저장소 이름)" "(branch 이름)"
    
#### pull
    git pull
    
+ pull 할 것이 있을 때 push를 하면?
    + 원격에 먼저 적용된 새 버전이 있으므로 적용 불가
    + pull 해서 원격의 버전을 받아온 다음 push 가능

#### local의 강제 내용 push하기
    git push --force
    
## 원격의 브랜치 다루기
+ 원격 branch 만들기
    + 1. local에서 branch 만들어 원격으로 push
    + 2. github에서 생성

#### local과 원격의 브랜치들 확인
    git branch --all
    
#### 원격의 변경사항 확인
    git fetch
    
#### local에 같은 이름의 branch를 생성하고 연결 그리고 switch
    git switch -t "(원격 저장소 이름)"/"(원격 branch 이름)"
    
#### 원격의 branch 삭제
    git push "(원격 이름)" --delete "(원격의 브랜치명)"
    
    



