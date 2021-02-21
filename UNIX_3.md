# UNIX_3 문제풀이

**1. 소유자가 george이고 그룹이 others일때 data파일의 소유자와 그룹을 동시에 변경하시오.**

```bash
$ chown george:others data

# chown : change owner 
```

**2. 현재 로그인한 사용자의 목록에서 2016-01-07에 접속한 사용자를 출력하시오.**

```bash
$ who | grep '2016-01-07'
```

**3. 접근권한이 775인 data 디렉토리를 생성하시오.**

```bash
$ mkdir -m 755 data

# -m : 디렉토리의 접근 권한을 설정한다. -m옵션은 디렉토리의 mod를 설정
```

**4. 현재 디렉토리에서 링크 파일만 찾는 lnfind란 alias를 생성하시오.**

```bash
$ alias lnfind='find ./ -type l'
```

**5. 현재 디렉토리에서 24시간 이내에 수정된 파일을 찾으시오.**

```bash
$ find ./ -mtime -1
```

**6. 현재 디렉토리에서 test로 시작하는 디렉토리만 찾아 삭제하시오. ??**

```bash
$ rm -r `find -name 'test*' -type d'

# 실행 못함  ㅠ ㅠ 
```

**7. ssh를 이용하여 kumquat라는 서버에 /test2라는 디렉토리를 생성하시오.**

```bash
$ ssh root@kumquat mkdir /test2
```

**8. test1 과 test2 의 내용을 비교하는 명령어를 작성하시오.**

```bash
$ diff test1 test2
```

**9. test1 test2 test3을 리다이렉트를 이용하여 test4의 파일로 합치시오.**

```bash
$ cat test1 test2 test3 > test4

# cat : 파일 내용 출력, 파일 생성, 파일 병합  
```

**10. test5 파일의 마지막 10개의 행을 출력하시오.**

```bash
$ tail test5
```

**11. /etc/group 과 /etc/password에서 root가 있는 라인의 개수를 출력하시오.**

```bash
$ grep -c 'root' /etc/group/* /etc/password/*
```

**12. test6파일에서 시작문자가 a, 마지막 문자가 z로 끝나는 문장을 출력하시오.**

```bash
$ grep -e '^a' test6 | grep -e 'z$'

$ grep -E '^a.*z$' test6
```

ㄴ ** grep 참고

[[Linux] grep, egrep, fgrep](https://myinfrabox.tistory.com/48)

**13. test6파일에서 mail이 나오는 행과 plug가 나오는 행 사이의 모든 행을 출력하시오.**

```bash
$ sed -n '/mail/, /plug/ p' test6

# -n : 읽어들인 라인을 암시적으로 자동출력하는 것을 중단한다. 
#  p : 행을 출력한다.  
```

**14. test7파일을 gzip으로 압축하시오.**

```bash
# 형식

# 압축하기 
# tar -cvf [파일명.tar] [압축할 파일 또는 폴더명]

# 압축풀기
# tar -xvf [파일명.tar]

$ tar -cvf test7.gzip test7

# 옵션 
# -c : 파일을 tar로 묶음
# -p : 파일 권한을 저장
# -v : 묶거나 파일을 풀 때 과정을 화면으로 출력
# -f : 파일 이름을 지정
# -C : 경로를 지정
# -x : tar 압축을 풂
# -z : gzip으로 압축하거나 해제함
```

**15. test8 파일의 가장 긴 줄의 길이를 출력하시오.**

```bash
$ wc -L test8
```

**16. vi ex에서 10행부터 파일의 끝까지를 test9로 저장하시오.**

```bash
:10,$ w test9

# $ : 마지막 행 
```

**17. vi ex에서 help 또는 Help를 모두 HELP로 변경하시오**

```bash
:%s/[hH]elp/HELP/
```

**18. dd를 사용하여 블록사이즈가 2바이트이고 10블록의 null문자로 채워진 test10파일을 생성하시오.**

```bash
$ dd if=/dev/zero of=test10 bs=2 count=10

# 형식
$ dd if=/dev/zero of=파일명 bs=1GB count=10

# dd는 파일을 변환하고 복사하는 명령어이다.

# $ dd if=입력 of=출력 bs=바이트 count=반복

# ibs = bytes     #한번에 bytes 바이트씩 읽는다.
# obs = bytes     #한번에 bytes 바이트씩 쓴다.
# skip = n        #n*ibs 바이트만큼 무시하고 읽는다.
# seek = n        #n*obs 바이트만큼 무시하고 쓴다.
```

**19. test11파일의 3번째 필드를 기준으로 정렬하시오.**

```bash
$ sort -k 3 test11

# -k : 지정한 필드 기준으로 정렬
```

**20. test12 파일을 역순으로 정렬하고 중복되는 라인을 제거하고 출력하시오** 

```bash
$ sort -ur test12

# -r : 역순 정렬
# -u : 정렬 후, 중복행 제거 
# -n : 라인의 각 필드를 비교하는 대상을 숫자로 한정 
# -f : 영어를 정렬할 때, 대소문자 구별안함 
# -b : 앞에 붙는 공백 무시
# -t : 필드 구분자 지정
# -m : 정렬된 파일을 병합
# -o : 저장할 파일명을 명시, 명시하지 않으면 화면에 출력

# 출처: https://linuxmadang.tistory.com/entry/linux리눅스-sort-명령어 [리눅스마당]
```

**21. 월요일마다 새벽4시 30분에 /bin/date를 실행하는 cron문을 작성하시오**

```bash
30 4 * * 1 /bin/date

#    *　　　　　　*　　　　　　*　　　　　　*　　　　　　*
# 분(0-59)　　시간(0-23)　　일(1-31)　　월(1-12)　　　요일(0-7)

# cron : 주기적으로 작업을 실해아는... 그런 것... 
```

**22. 최근에 사용한 명령 20개를 출력하시오.**

```bash
$ history 20
```

**23. cut 명령어로 test14파일의 “_“를 구분자로 지정하여 두번째 필드를 출력하시오.**

```bash
$ cut -d"_" -f2 (X)

$ cat test14.txt | cut -d"_" -f2 (○)
$ cut -d"_" -f2 test14.txt (○)

# cut : 파일에서 필드를 뽑아내는 명령어, 기본 구분자는 탭

#  옵션 
# - d: 구분자를 지정한다
# - f: 잘라낼 필드를 지정한다
# - c: 잘라낼 곳의 글자 위치를 지정한다
# - s: 필드 구분자를 포함할수 없다면 그 행은 수행하지 않는다
```

**24. touch 명령어를 이용하여 test15파일을 2016년 1월 1일로 변경하시오.**

```bash
$ touch -t 201601010000 test15 

# -touch
# 옵션을 지정하지 않으면 크기가 0인 파일을 생성

# 옵션
# -t :  : 파일의 날짜 정보 변경 , YYYYMDDhhmm 형식 
# -c : 현재 시간으로 변경
# -r: 뒤에 따라오는 파일의 시간과 같게 변경
#     (touch -r 1번 2번 => 2번 파일이 1번과 같게 변경됨)
```

**25. nginx 프로세스에 대한 정보를 출력하시오.**

```bash
$ ps -ef | grep nginx

# ps -ef : cpu 사용률과 사용중인 프로세스 체크 
```

**26. 2342의 PID를 가진 프로세스를 종료하시오.**

```bash
# 형식
# $ kill 종류 PID
$ kill -15 2342

# -15 : 정상 종료
# -9 : 강제 종료 
```

**27. ls를 백그라운드로 동작시키시오.**

```bash
$ ls &

# & :  백그라운드 실행. 실행되는 동안 다른 일을 하기 위해서 사용 
```

**28. 백그라운드 작업목록을 출력하시오.**

```bash
$ jobs 
```

**29. test16의 파일을 test.tar로 압축하시오.**

```bash
$ tar -cvf test.tar test16

# 압축하기 
# tar -cvf [파일명.tar] [압축할 파일 또는 폴더명]

# 압축풀기
# tar -xvf [파일명.tar]

# 옵션 
# -c : 파일을 tar로 묶음
# -p : 파일 권한을 저장
# -v : 묶거나 파일을 풀 때 과정을 화면으로 출력
# -f : 파일 이름을 지정
# -C : 경로를 지정
# -x : tar 압축을 풂
# -z : gzip으로 압축하거나 해제함
```

 

**30. 일정한 크기를 가진 여러 개의 작은 파일로 분할하는 명령어를 이용하여  test17 파일을 20행 씩 분할하시오.** 

```bash
$ split -l 20 test17

# split : 파일을 분할하는 명령어 

# 파일을 10m단위로 분할한다.
$ split -b 10m test17 

# 파일을 10줄 단위로 분할한다.
$ split -l 10 test17    
```

**31. memory의 상세정보를 볼 수 있는 파일의 위치를 작성하시오.**

```bash
$ which free
```

**32. 명령어의 위치를 찾을 수 있는 명령어를 작성하시오.**

```bash
$ which
$ whereis
```

**33. 60초 동안 대기하는 명령어를 작성하시오.**

```bash
$ sleep 60
```

**34. /dev/sda5 를 /mnt 에 마운트하는 명령어를 작성하시오.**

```bash
# 형식 
# mount [OPTION] [DEVICE] [PATH]

$ mount /dev/sda5 /mnt

# mount : 장착되어있는 디바이스를 마운트하는 명령어이다. 
# 마운트 : 하드웨어 장치를 특정 위치, 즉 디렉토리에 연결시켜주는 과정
```

**35. 작업중인 터미널 창이 종료되더라도 실행중인 프로세스를 백그라운드 프로세스로 계속 작업할 수 있도록 하는 명령어를 작성하시오.**

```bash
$ nohup [실행 스크립트] &

# nohup : 세션이 끊기더라도 실행을 멈추지 않고 동작하도록 함 
# &     : 프로세스를 실행할 때 백그라운드에서 동작하도록 만드는 명령어  
```

**36. apt-get 명령이 패키지 관련 정보를 확인하기 위해 참조하는 파일의 위치를 작성하시오.** 

```bash
/etc/apt/sources.list
```

**37. yum 을 이용하여 nginx 패키지를 제거하는 명령어를 작성하시오.** 

```bash
# 형식
# yum [옵션] [명령] [패키지명]
$ yum remove nginx

# yum(Yellodog Update Modified) : 레드햇 계열의 리눅스 배포판에서 사용하는 
#                                 프로그램(패키지) 설치 관리 도구 

```

**38. 커널에 로드되어있는 모듈을 확인하는 명령어를 작성하시오.**

```bash
$ lsmod
```

**39. 현재 파일시스템들의 사용량을 MB단위로 출력하시오.**

```bash
$ df -m

# df : Disk Free 의 약어. 현재 사용중인 파일시스템의 전체 크기, 사용 중인 크기, 
#     사용 가능한 크기, 사용률, 마운트 정보 등을 보여준다.

# -m : mb 단위
# -k : kb 단위 
```

**40. /home/test18 디렉토리의 사용량을 KB단위로 출력하시오.**

```bash
# 형식
# du [option] [file..]
$ du -k ./home/test18

# du : Disk Usage 의 약어.
#      df 명령어가 시스템 전체의 디스크 공간을 확인하는 명령어라면, 
#      du 명령어는 특정 디렉토리를 기준으로 디스크 사용량을 확인할 수 있다. 

# -k : kb 단위로 표시
# -h : 사람이 읽기 좋게 파일 단위 표시

# 참고 : https://jhnyang.tistory.com/301
```

**41. awk를 사용하여 test19파일의 필드 개수를 출력하시오.**

```bash
$ awk '{print NF}' test19

# awk가 내부적으로 사용하는 시스템 변수

# FILENAME	현재 처리중인 파일명
# FS	필드 구분자로 디폴트는 공백
# RS	레코드 구분자로 디폴트는 새로운 라인
# NF	현재 레코드의 필드 개수
# NR	현재 레코드의 번호
# OFS	출력할 때 사용하는 FS
# ORS	출력할 때 사용하는 RS
# $0	입력 레코드의 전체
# $n	입력 레코드의 n번째 필드
```

**42. awk를 이용하여 test20파일의 “_“를 구분자로 하는 첫번째와 세번째 필드를 출력하시오.**

```bash
# 형식
# awk [-f 프로그램파일] [-F 필드구분자] ['패턴{액션}'] [처리할 파일명]

$ awk -F_ '{print $1 $3}'./test20
```

**43. cat nofile의 표준에러를 표준출력으로 리다이렉트하시오.**

```bash
$ cat nofile 2>&1 

# 표준 에러(STDERR) 
# : 프로그램이 오류 메시지나 진단을 출력하기 위해 일반적으로 쓰는 출력 스트림
#   표준 추력과 독립적인 스트림이며, 별도로 리다이렉트 가능하다. 
#   표준 에러의 파일 디스크립터는 2다.

# 표준 출력(STDOUT)
# : 프로그램이 출력 데이터를 기록하는 스트림.
#   표준 출력의 파일 디스크립터는 1이다. 

# 표준 입력 : 파일 디스크립터 0 

# 표준 출력을 버림( /dev/null 로 redirect )
$ ./program 1>/dev/null

# 표준 에러를 버림( /dev/null 로 redirect )
$ ./program 2>/dev/null

# 참고 : https://blogger.pe.kr/369
```

**44. basename /home/mkel/bin/test.sh의 결과값을 작성하시오.**

```bash
test.sh

# basename : 경로명과 파일명을 분리해 파일명을 출력해주는 명령어
```

45. test21의 계정의 로그인 쉘을 sh 로 변경하시오. ?? 

```bash

```

**46. 시스템 부팅 시 자동으로 마운트되게 하기 위해서 설정해야 하는 파일의 위치를 작성하시오.**

```bash
/etc/fstab

# /etc/fstab
# : 파일시스템 정보를 저장하고 있으며 리눅스 부팅 시 마운트 정보를 저장하고 있다. 

# 참고 : https://daily50.tistory.com/174
```

**47. 호스트끼리 메일 메시지를 주고받기 위한 간단하고 확장성이 있는 프로토콜은 무엇인가?**

→ sendmail 

: 인터넷 전자 메일의 표준 규약인 SMTP(Simple Mail Transfer Protocol) 프로토콜을 통해서 메일 서버 간에 메일을 주고 받는 역할을 한다. 

참고 : [https://securitymax.tistory.com/132](https://securitymax.tistory.com/132)

**48. www.amazon.com 의 DNS를 질의할 수 있는 명령어를 작성하시오.**

```bash
$ nslookup www.amazon.com

# nslookup : DNS 서버에 질의를 하는 명령어. DNS 서버와 대화식으로 질의하고 응답을 받는다.
# DNS : Domain Name System 의 약어. 사람이 읽을 수 있는 도메인 이름을 머신이 읽을 수 있는 IP 주소로 변환한다.
#       ex) www.amazon.com → 192.0.2.44 
```

**49. listen되고 있는 포트의 네트워크 정보 상태를 출력하시오.**

```bash
$ netstat -tnlp 

# netstat : 네트워크 연결상태, 라우팅테이블, 인터페이스 상태 등을 보여주는 명령어

# 옵션 
# -t : TCP 프로토콜만 출력 
# -n : 도메인 주소를 숫자로 출력 
# -l : 대기중인 네트워크[--listening]
# -p : PID(프로세서ID)와 사용중인 프로그램명 출력[--program]
# : 
# : 

# 참고 : https://websecurity.tistory.com/103
```

**50. bash에서 2MB보다 큰 파일을 만들지 못하게 하는 명령어를 작성하시오.**

```bash
$ ulimit -f 2000 # kb 단위 

# ulimit : 프로세스의 자원 한도를 설정하는 명령. 

# 옵션 
# -a : 모든 제한 사항을 보여준다.
# -c : 최대 코어 파일 사이즈
# -d : 프로세스 데이터 세그먼트의 최대 크기
# -f  : shell에 의해 만들어질 수 있는 파일의 최대 크기
# -s : 최대 스택 크기
# -p : 파이프 크기
# -n : 오픈 파일의 최대수
# -u : 프로세스 최대수
# -v : 최대 가상메모리의 량
```
