# Docker-Tips
Docker 사용법

### Docker
* Docker Install
  ```
  $ sudo apt-get install docker
  ```

* Nvidia-Docker Install
  ```
  $ sudo apt-get install -y nvidia-docker2
  $ sudo pkill -SIGHUP dockerd
  ```

* sudo 없이 사용
  * 커맨드 입력 후 터미널을 재시작해야 적용됨
  ```
  $ sudo usermod -aG docker $USER
  ```

* Docker Image Download
  * Docker Image 이름은 [Docker Hub](https://hub.docker.com/)에서 검색 가능
  ```
  $ docker pull <DOCKER_IMAGE_NAME>
  (example)
  $ docker pull nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04 (NVIDIA에서 배포한 UBUNTU 16.04 OS에 CUDA 8.0, CUDNN 6이 설치된 Docker Image)
  ```

* Docker Image list (installed)
  ```
  $ docker images
  ```

* Docker running container list
  ```
  // 실행 중인 것만
  $ docker ps

  // 모두
  $ docker ps -a

  // 명령어 짤림 없이
  $ docker ps -a --no-trunc
  ```

* Docker build
  ```
  $ docker build . -t <docker_id>/<repository>:<tag>
  ```
  * build 파일 예제
    ```
    파일 이름 : Dockerfile
    --------------------------
    FROM tensorflow/tensorflow:1.10.0-gpu-py3	// IMAGE의 default 환경

    RUN rm -rf /etc/apt/sources.list
    RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial main restricted universe multiverse" >> /etc/apt/sources.list
    RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list
    RUN echo "deb-src mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list
    RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list
    RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-security main restricted universe multiverse" >> /etc/apt/sources.list
    RUN apt-get -y update
    RUN apt-get -y install language-pack-ko
    ENV LANG ko_KR.UTF-8
    
    RUN mkdir /mrc-service 		// 커맨드 실행
    WORKDIR /mrc-service		// 작업 폴더 변경
    ADD mrc-service /mrc-service	// 폴더 복사
    RUN pip install -r requirements.txt
    ```

* Docker container to images
  ```
  $ docker commit <container_name> <repository>:<tag>
  ```

* Docker image to file
  ```
  $ docker save -o <path/for/tar_file> <image_name>
  ```

* Docker load from file
  ```
  $ docker load -i <path/to/tar_file>
  ```

* Docker images 삭제
  ```
  $ docker rmi <image_name>
  ```

* Docker run 
  ``` 
  // Run bash
  $ docker run -it <repository>:<tag> bin/bash

  // Run command
  $ docker run -it <repository>:<tag> bin/bash -c "<command>"

  // Run with Port
  $ docker run -it -p host_port:container_port <repository>:<tag> bin/bash -c "<command>"
  // one more
  $ docker run -it -p host_port_1:container_port_1 -p host_port_2:container_port_2 <repository>:<tag> bin/bash -c "<command>"

  // Run Background
  $ docker run -i -d ...

  // 이름 설정
  $ docker run -it --name <name_of_container> ...
  ```

* Docker copy with container
  * docker path : container_name:/path/file
  ```
  $ docker cp <path/for/from/file> <path/for/to/file>
  ```

* Docker log
  ```
  $ docker log <container_name>
  ```

* Docker stop
  ```
  $ docker stop <container_name>
  ```

* Docker start/restart
  ```
  $ docker start/restart <container_name>
  ```

* Docker container 삭제
  ```
  $ docker rm <container_name>
  ```


### Docker Hub
* [Docker Hub](https://hub.docker.com/)

* Docker login
  ```
  docker login
  ```

* Docker Image upload
  ```
  docker push <docker_id>/<repository>:<tag>
  ```





