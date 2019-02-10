---
layout: post
title:  "Linux Command"
subtitle: "리눅스 명령어 모음"
type: "Linux"
date: 2019-01-11 13:14:00
development: true
text: true
author: "Choi corder"
---

리눅스 명령어 모음(Linux Command Set)
=======

기본 명령어
-------

**login - 사용자 인증과정**  
리눅스 시스템은 기본적으로 multi-user 개념에서 시작하였기 때문에 시스템을 이용하기 위해서는 반드시 로그인을 하여야 합니다.

**passwd - 패스워드 변경**  
리눅스, 특히 인터넷의 세계에서는 일반 컴퓨팅 상황에 비하여 훨씬 해킹에 대한 위험이 높습니다. 패스워드는 완성된 단어 보다는 단어 중간에 숫자나 키보드의 ^, #, ' 등과 같은 쉽게 연상 할 수 없는 기호를 삽입하여 만들어 주는 것이 좋습니다.


**du - 하드 사용량 체크(chkdsk)**  
- 자신의 하드공간을 알려면  
`# du`
- 특정 디렉토리의 사용량을 알려면  
`# du -s diretory_name`

**ls - 파일 리스트 보기(dir)**  
> F : 파일 유형을 나타내는 기호를 파일명 끝에 표시  
>     (디렉토리는 '/', 실행파일은 '*', 심볼릭 링크는 '@'가 나타남).  
> l  : 파일에 관한 상세 정보를 나타냅니다.  
> a : dot 파일(.access 등)을 포함한 모든 파일 표시.  
> t  : 파일이 생성된 시간별로 표시  
> C : 도스의 dir/w명령과 같 이 한줄에 여러개의 정보를 표시  
> R : 도스의 dir/s 명령과 같이 서브디렉토리 내용까지.  
`# ls -al`
`# ls -aC`
`# ls -R`

**cd - 현재 디렉토리 위치 변경**  
- 하위 디렉토리인 bin으로 들어갈때  
`# cd /bin`
- 상위디렉토리로 이동  
`# cd  ..`
- 어느곳에서든지 자기 홈디렉토리로 바로 이동  
`# cd 또는 cd ~`
- 현재 작업중인 디렉토리의 하위나 상위 디렉토리가 아닌 다른 디렉토리(webker)로 이동하려면 /로 시작해서 경로이름을 입력하면 된다.  
`# cd /webker`


**cp - 파일 복사(copy)**  
index.html 화일을 index.old 란 이름으로 복사.  
`# cp index.html index.old`

test 디렉토리내의 모든 화일을 현 디렉토리로 복사.  
`# cp /home/test/*.*`


**mv - 파일이름(rename) / 위치(move)변경**  
- index.htm 화일을 index.html 로 이름 변경  
`# mv index.htm index.html`
- 파일의 위치변경  
`# mv file  ../main/new_file`


**mkdir - 디렉토리 생성**  
- download 디렉토리 생성  
`# mkdir download`


**rm - 파일 삭제**  
- test.html 파일 삭제  
`# rm test.html`
- 디렉토리 전체를 삭제  
`# rm -r <디렉토리>`
- a로 시작하는 모든 파일을 일일이 삭제할 것인지 확인하면서 삭제   
`# rm -i a.* `


**rmdir - 디렉토리 삭제**  
- cgi-bin 디렉토리 삭제  
`# rmdir cgi-bin`

**pwd - 현재의 디렉토리 경로**  

**put - ftp 상태에서 파일 업로드**  
`# put  guestbook.tar.gz`

**get - ftp 상태에서 파일 다운로드**  
`# get  guestbook.tar.gz`

**mput or mget - 여러개의 파일을 올리고 내릴때 사용(put과 get사용법과 동일)**  
리눅스에서는 각 화일과 디렉토리에 사용권한을 부여.

**chmod - 파일 권한 변경**  
  
| Owner | Group | Other |  
|:----- |:-----:|:-----:|  
| rwx   | rwx   | rwx   |  
| 7     | 7     | 7     |  
| 7     | 5     | 7     |  

ls -al
예) -rwxr-xr-x   guestbookt.html
rwx  :처음 3개 문자 = 사용자 자신의 사용 권한
r-x  :그다음 3개 문자 = 그룹 사용자의 사용 권한
r-x  :마지막 3개 문자 = 전체 사용자의 사용 권한

읽기(read)---------- 화일 읽기 권한
쓰기(write)---------- 화일 쓰기 권한
실행(execution)---------- 화일 실행 권한
없음(-)---------- 사용권한 없음

명령어 사용법
chmod 변경모드 파일
- test.html 화일을 자신에게만 r,w,x 권한을 준다.
`# chmod 666  guestbook.html
- 자신은 모든 권한을 그룹사용자와,전체사용자에게는 읽기와 쓰기 권한만 준다.
`# chmod 766  guestbook.html

**alias - 명령어 별명 짓기**  
" doskey alias" 와 비슷하게 이용할 수 있는 쉘 명령어 alias는 말그대로 별명입니다. 사용자는 alias를 이용하여 긴 유 닉스 명령어를 간단하게 줄여서 사용할 수도 있습니다. 이들 앨리어스는 [alias ls 'ls -al'] 같이 사용하시면 되는데, 한 번 지정한 alias를 계속해서 이용하시려면, 자신의 홈디렉토리에 있는 .cshrc(Hidden 속성)을 pico등의 에디터를 이용하여 변경시 키면 됩니다.

**cat - 파일의 내용을 화면에 출력하거나 파일을 만드는 명령**  
`# cat filename`

**more - cat과 동일한 기능을 하지만, 화면 단위로 넘어서 출력해준다.**  
`# more <옵션>`
옵션은 다음과 같습니다.

> Space bar : 다음 페이지  
> Return(enter) key : 다음 줄  
> v : vi 편집기로 전환  
> /str : str 문자를 찾음  
> b : 이전 페이지  
> q : more 상태를 빠져나감  
> h : 도움말  
> = : 현재 line number를 보여줌  

**who - 현재 시스템에 login한 사용자의 리스트를 보여준다.**  
`# who`

**whereis - 소스, 실행파일, 메뉴얼 등 위치를 검색할때 사용**  
- perl의 위치를 알려준다  
`# whereis perl`

**vi - 리눅스 상의 에디터**  
- vi 편집기 상태로 들어감  
`# vi newfile`

**cat, head, tail - 파일 내용만 보기**  
- 파일의 내용을 모두 보여줌  
`# cat filename`
- n줄 만큼 위세서부터 보여줌  
`# head -n filename`
- n줄 만큼 아래에서부터 보여줌  
`# tail -n filename`