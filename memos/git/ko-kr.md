# git
1. 철저히 '본인' 의 기준에 맞춰 작성한 Git 사용 관련 메모들입니다.
2. [다음 저장소에 있는 내용](https://github.com/Yuny2036/TIG/blob/main/memos/git/ko-kr.md)을 가져왔습니다. 

## 일단 Repository 생성
1. Git을 쓸 생각이 있고
2. Github에 원격으로 저장할 생각이 조금이라도 있다면
3. **어차피 만들거 아닌가?** 🤔
4. 그러니 그냥 와서 만들고 봅시다. 개설할 때 돈 드는거 아니니까.

##  'README.md 만들기', '.gitignore'
1. **어차피 쓸 거고** 🤔
2. 공짜로 해준다면
3. 그냥 하면 되잖아요
4. 게다가 저 둘은 간단한 문서라서 그냥 여기서 고쳐도 돼..

## commit, push
1. commit하고
2. push하고
3. **안하면 여기까지 안 올라온다.**

## 네이밍과 메시지
1. 기능 단위로 브랜치를 나눌 때는 `feature/기능-요약`, `fix/버그-요약` 형식을 유지한다.
2. 제목 줄은 최대 50자 이내로 작성하고, 한 줄 띄운 후 본문에서 상세 내용을 기술한다.

-----
-----
# git 명령어 메모
## git 관리하기
1. git --version : git의 버전을 확인함
2. **git config** : git의 설정을..
   > git config --list : git 의 설정을 나열함  
   > git config --global : git 설정을 사용자 공통, 전역으로 적용
   >> \[attributes] \[attributes' value] : \[attributes] 의 값을 \[attributes' value] 로 변경

## 저장소 초기화하기
1. git init : 로컬에 빈 저장소 생성
2. git remote add origin \[remote repository] : 원격 저장소 \[remote repository] 를 로컬 저장소와 연결함
3. git remote remove origin : 로컬 저장소에 연결된 원격 저장소를 연결 해제함

## 저장소 관리하기
1. git status : 현재 git 상태를 확인함
2. git log : 저장소의 변경이력을 살펴봄

## 로컬에서 원격으로
1. git add : 스테이지에 변경사항을 등록
> git add . : **현재 디렉터리·하위 디렉터리**의 *추가·수정* 파일을 스테이징(삭제-파일 제외)  
> git add -A : 저장소 전체에서 *추가·수정·삭제* 모든 변경사항을 스테이징
2. **git commit -m \[message]** :  
   스테이지에 올라간 변경사항을 원격 저장소에 적용할 준비를 함, commit 메시지는 \[message] 로 남김
> git commit --amend -m \[message] : commit 메시지를 \[message] 로 변경
3. **git push** :  
   커밋한 항목들을 원격 저장소에 적용
> git push -u \[remote repository] \[current branch name] :  
> \[current branch name] 이름의 현재 브랜치를 \[remote repository] 의 \[current branch name] 브랜치와 연결.
>> 원격 저장소의 브랜치와 같은 이름의 로컬 저장소의 브랜치를 merge 할 수 있게 함
4. **git remote** :  
   원격 저장소를 가리킴
> git remote -v : 연결된 원격 저장소의 주소를 출력함  
> git remote add \[name] \[remote-url] : \[name] 을 이름으로 하여 \[remote url] 주소의 원격 저장소를 연결함
> git remote rename \[old-name] \[new-name] : 원격 저장소의 예전 이름 \[old-name] 을 새 이름 \[new-name] 으로 변경함
> git remote set-url \[name] \[new-url] : 원격 저장소 \[name] 의 주소를 \[new-url] 로 변경함
> git remote remove \[name] : \[name] 이름의 원격 저장소 연결을 해제함

## 저장소간의 버전이 다른 상황에서의 작업
1. git pull : 원격 저장소의 앞서가는 버전을 로컬 저장소에 적용함
2. git reset --hard \[commit ID] : ⚠️ 로컬의 모든 변경사항을 삭제하고 \[commit ID] 상태로 되돌림(주의!)

## 브랜치 BRANCH, 체크아웃 CHECKOUT, 머지 MERGE
1. git branch : 브랜치 목록 확인
> git branch <name> : ‘name’ 으로 브랜치 생성 
> git branch -d <name> : ‘name’ 이름의 브랜치 제거  
> git branch -D <name> : 강제 삭제
2. git checkout <name> : ‘name’ 이름의 브랜치로 이동(이동한 브랜치가 HEAD, 그러니까 현재 브랜치가 되고, 해당 브랜치에서 작업하게 됨)
> git checkout -b <name> : ‘name’ 이름의 브랜치로 생성한 뒤 이동
3. git merge <name> : 'name' 이름의 브랜치를 현재 작업중인 브랜치(HEAD)에 병합
> git merge --no-ff <name> : 병합 커밋 강제 생성