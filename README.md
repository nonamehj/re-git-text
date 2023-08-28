# re-git-text

내 컴퓨터에 항상 등록을 시켜줘야한다.

@)처음 등록 방법
git config --global user.name"이름"
git config --global user.email"이메일"

@)등록한거 확인 방법
git config --list
---------------------------
@ 3가지 Working Directory, Staging area, Repository
1)Working Directory(작업공간) ->작업하는곳
2)Staging area ->추가,변경을 임시 저장하는곳
3)Repository(실제저장소) ->staging area저장한것을 저장완료시킴

- git init  = 깃시작
- git init = 깃시작
- git status =현재 깃의 staging area상태를 보는 명령문
- git add 파일명 (or . ) 해당파일을 staging area에 추가
- git add . 모든 파일을 staging에 추가
- git rm --cached 파일명 = 해당 파일을 staging area에 삭제
- git commit -m "메세지" = 깃을 레파지토리에 저장
- git log = 커밋 이후 변경 로그를 확인
  * git log --all --oneline --graph
  (전체 한줄 그래프 모양)
--------------------------------
@원격저장소 저장

git remote add origin 본인깃계정 => 원격저장소를 추가한다
git push origin master => 원격저장소에 저장한다

원격저장주소가 길거나 복잡하면 변수로 사용 하는 방법
git remote add origin 깃계정(깃허브에 올릴 주소)
=>origin 으로 변수명 주고 편리하게 사용이 가능하게 해줌

git push -u origin main (또는 master) => 원격저장소에 저장
(한번 -u 사용했으면 git push 만 해줘도 가능하다)
(원격저장소 주소 뒤에 .git 으로 끝내야 한다)
main 에서 master , master 에서 main 바꾸는 방법
=> git branch -M master
=> git branch -M main
------------------------------------
@reset 방법 3가지(--hard, --mixed, --soft)

git reset --hard (--mixed, --soft) HEAD^
* HEAD^, HEAD^^, HEAD^^^
^1단계 되돌리기 ^^ 2단계되돌리기 ^^^ 3단계 되돌리기

1) --hard (위험성은 높음, 잘 쓰면 매우 좋은 --hard)
git reset --hard HEAD^
=> 커밋을 한단계 앞으로 되돌린다(모두 초기화)
=> 작업하고 있던 작업물, 스테이징에 올렸던 추가물, 한번 저장했던 레파지토리 이력이 전부다 사라진다
(그만큼 위험하고 잘 사용해야한다)

ex)
레파지토리에 : text1, text2, text3  (순서는 왼쪽부터)
스테이징에어리어 : text1,text2,text3
워킹디렉토리 : text1,text2,text3

git reset --hard HEAD^^ (두단계 일경우)
처음 레파지토리에 올린 text1 내용만 남아 있고 나머지 기록들은 다 사라진다

git reset --hard HEAD^ (한단계 일경우)
레파지토리에 처음에 올린 text1, text2 내용만 남아 있고 나머지 기록은 다 사라진다

=> git log로 확인해보면 되돌린 커밋 확인해서 알 수 있다 

2) --mixed (default 기본값 기본적으로 사용함)
git reset --mixed HEAD^
= 현재작업하고 있던(워킹디렉토리) 작업물은 그대로 남아 있다
(스테이징 하고 레파지토리가 지워진다)
=커밋을 한단계 앞으로 되돌린다(working directory는 유지)
=작업공간은 보존하고 스테이징, 레파지토리 의 커밋이력이 한단계 되돌려진다

ex)
레파지토리에 :text1, text2 (왼쪽부터 올린 순서)
스테이징에어리에 : text3
워킹디렉토리에 :text1 (추가 내용)

=> text1, text2, text3 내용은 다 남아 있고 레파지토리에 text2는 없어진다.
=> 워킹디렉토리에 추가 수정한 내용은 남아 있어야 한다.

git log 에서 확인하면 text1 커밋한것만 보여짐
git status 확인하면 중간에 올린 작업물들이 다 빠진다.
(스테이징에 올린 text3, 레파지토리 text2 다 빠져 버린다)


3) --soft
git reset --soft HEAD^

ex)
레파지토리에 : text1, text2  (왼쪽부터 올린순서)
스테이징에어리어 : text1(추가 내용)
워킹디렉토리 : text1 추가 내용

=>변화는 거이 없다.  레파지토리에 올린 text2만 없어지고 내용물은 전부 그대로 남아있다.

git log  에서확인하면 text2 레파지토리에서 없어진다.
스테이징에어리어에는 text1(스테이징까지한내용), text2(레파지토리에 올리기 전으로) 으로 돌아간다
결국 마지막 커밋한게 지워진다.

--------------------------------
@branch
=>하나의 라인으로 만드는게 아니고 branch(나뭇가지)로 만들어서 따로 만들어냄

브랜치를 나누기 전에 최소한 한번이라도 commit 이루어져야함
git branch 브랜치저장할이름 -> 브랜치 생성
git branch ->브랜치 확인
git switch 브랜치저장했던이름 
(or git checkout 브랜치저장했던이름) -> 브랜치 변경
git branch -D 이름 -> 브랜치 삭제
git merge 합치는 브랜치명 -> 병합

=>git branch A 만들고 난후 새로 파일 만들고  다시 master로 돌아가면 새로 만든 파일이 없어진다 (사라지는게 아니다)

@merge 병합
merge 할 때 합치고 싶은 브랜치로 들어가서 merge 사용
branch 작성한것을 main 하고 합치고 싶다면
git checkout main 으로 들어가서 git merge 합칠브랜치명 한다.

(main 안에 A 브랜치가 들어와 있음)

- 사용한 branch 삭제 방법
git branch -D 삭제할브랜치명

--------------------------------------
@원격자정소와 상호작용
(로컬 저장소의 상태와 원격저장소(git hub)의 상태를 동일하게 맞춘다!)
remote =원격저장소에 조회(추가)하기
push = 원격저장소에 밀어넣기
pull = 원격저장소에 얻어와서 합치기
fetch = 원격저장소에서 열기
clone = 원격저장소에 복사하기

git remote -v 로  등록한 주소를 확인 할 수 있다

- git remote add 단축이름  주소
=>git remote add origin 깃허브 원격주소
(origin 주로 단축으로 많이 씀)



- git push -u origin master(or main)  =>마스터브랜치로 올리겠다
ex)
만약 A브랜치에서 push 하겠다면
git push origin A 하면 된다

- git pull origin master 
  (origin에 있는 master 브랜치를 가져와라)
= 땡겨와서 머지 시킨다
= 원격저장소의 origin의 master브랜치를 가져와서 합쳐라

- git fetch origin master (주로 다른거와 비교할때)
  (origin에 있는 master 브랜치를 가져와라)
= 가져오는데 합치지 않고 일단가져오기
= 가져오면 파일이 보이지는 않음
(임시 FETCH_HEAD (브랜치)or origin/master 확인) 둘중 하나 사용함
= 수동으로 머지 해야함
= fetch 하면 파일은 보이지 않음.. 임시브랜치에 저장을 해둠


만약 임시브랜치가  브랜치로 쓰일거면 git swtich -c 새로운 브랜치를 만들어서 브랜치로 사용하라 (직접볼수있게 사용함)
브랜치로 만들거 아니고 master에서 바로 머지 해도 상관없음
git merge (fetch에서 만들어준 임시 브랜치명)


-git clone 주소

= 통째로(원격저장소) 복사해서 가져옴
= 처음 새 컴퓨터에 프로젝트를 가져올때 사용함
= init 할 필요가 없음

