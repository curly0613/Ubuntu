# ubuntu-tips
ubuntu 사용법 (18.04 기준)

### CPU 정보 확인
```
$ cat /proc/cpuinfo

// CPU 전체 코어 수 확인
$ grep -c processor /proc/cpuinfo
```

### Update
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

### 한글
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

### Disk mount
* format disk
  * disk 이름은 'df -h' 또는 'fdisk'로 확인 가능
  ```
  $ mkfs.ext4 /dev/<disk_name>
  ```

* mount
  ```
  $ mount /dev/xvdb /1T
  ```

### Find
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
