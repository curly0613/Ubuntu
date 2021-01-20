# cuda-tips
cuda 사용법

### Cuda
* Cuda Install
  * Nvidia Driver
    - [다운로드](https://www.nvidia.co.kr/Download/index.aspx?lang=kr)
    ```
    $ sudo sh NVIDIA-Linux-x86_64-*.run
    ```

  * CUDA
    - [다운로드](https://developer.nvidia.com/cuda-toolkit-archive)
    ```
    $ sudo chmod +x cuda_9.0.176_384.81_linux.run
    $ ./cuda_9.0.176_384.81_linux.run --override

    // 대부분 accpet
    // BUT, Nvidia 드라이버는 설치 X (Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 384.81? -> "NO" )

    ```

  * Cudnn
    - [다운로드](https://developer.nvidia.com/rdp/cudnn-download)
    ```
    // 9.0 기준
    $ tar -zxvf cudnn-9.0-linux-x64-v7.1.tgz
    $ sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
    $ sudo cp  cuda/include/cudnn.h /usr/local/cuda-9.0/include/
    ```

  * libcupti
    ```
    $ sudo apt-get install libcupti-dev
    ```

  * 환경설정
    - ~/.bashrc
    ```
    ...
    export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    ```


### 참조
https://m.blog.naver.com/PostView.nhn?blogId=slehd219&logNo=221459958835&proxyReferer=https:%2F%2Fwww.google.com%2F