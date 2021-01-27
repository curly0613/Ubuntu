# ubuntu-tips
ubuntu 사용법 (18.04 기준)

### 바로가기
* [CPU 정보 확인](#cpu)
* [MEM 사용량 확인](#mem)
* [업데이트](#update)
* [한글](#korean)
* [마운트](#mount)
* [검색](#find)
* [쉘스크립트](#sh)

### <a name="cpu">CPU 정보 확인</a>
```
$ cat /proc/cpuinfo

// CPU 전체 코어 수 확인
$ grep -c processor /proc/cpuinfo
```

### <a name="mem">특정 프로세스 메모리 사용량 확인</a>
```
$ ps -eo pid,rsz,vsz,cmd | grep mongo | grep -v grep
```

### <a name="update">Update</a>
* Repository 추가
  ```
  $ apt install software-properties-common
  $ add-apt-repository ppa:deadsnakes/ppa
  $ apt update
  ```

* 갑자기 update 안될 때 (hash-sum mismatch)
  ```
  $ sed -i 's/archive.ubuntu.com/kr.archive.ubuntu.com/g' /etc/apt/sources.list
  ```

### <a name="korean">한글</a>
* 초기 설정
  ```
  $ apt install locales

  // ~/.bashrc 추가
  --------------------------------
  ...
  export LANGUAGE=ko_KR.UTF-8
  export LANG=ko_KR.UTF-8
  --------------------------------

  $ source ~/.bashrc
  $ locale-gen ko_KR ko_KR.UTF-8
  $ update-locale LANG=ko_KR.UTF-8
  $ dpkg-reconfigure locales
  ```

### <a name="mount">Disk mount</a>
* format disk
  * disk 이름은 'df -h' 또는 'fdisk'로 확인 가능
  ```
  $ mkfs.ext4 /dev/<disk_name>
  ```

* mount
  ```
  $ mount /dev/xvdb /1T
  ```

### <a name="find">검색</a>
  * 파일명으로 찾기
  ```
  $ find <dir> -name "<file_name>"

  ex) 현재 디렉토리 내에서 python 확장자를 갖는 파일 찾기
  $ find . -name "\*.py"
  ```

  * 파일 내 텍스트로 찾기
  ```
  $ grep "text" <file_name>

  ex) 현재 디렉토리 내에서 python 이라는 텍스트가 포함된 내용 찾기
  $ grep -r "python" *
  ```

### <a name="sh">Shell Script</a>
  - loop 문
  ```
  #!/bin/bash
  SET=$(seq 시작값 이동값 최종값)
  for i in $SET
  do
    # using command with "$i"
  done
  ```
