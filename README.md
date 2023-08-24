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
