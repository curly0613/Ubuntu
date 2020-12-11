# ubuntu-tips
ubuntu 사용법 (18.04 기준)

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


### Pyhton
* Python 3.6 설치
  ```
  $ apt install python3.6-dev
  ```

* Python 3.6 default 설정
  ```
  $ update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1
  ```

* pip install for version 3.6 (꼭! default 설정 후)
  ```
  $ wget https://bootstrap.pypa.io/get-pip.py
  $ python get-pip.py
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

