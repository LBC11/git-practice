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
    
