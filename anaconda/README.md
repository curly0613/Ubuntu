# Aanconda-Tips
Anaconda 사용법

### Anaconda
* Ananconda Install
  * https://repo.anaconda.com/archive/에서 버전 확인
  ```
  $ wget https://repo.anaconda.com/archive/Anaconda3-5.3.1-Linux-x86_64.sh 
  $ sudo sh Anaconda3-5.3.1-Linux-x86_64.sh
  ```

  * Install check
  ```
  $ source ~/.bashrc 
  $ conda list
  ```

* Anaconda Environment
  * create
  ```
  $ conda create --name "env_name" python="version, ex) 3.6"
  ```
  
* remove
  ```
  $ conda env remove --name "env_name"
  ```

  * activate
  ```
  $ conda activate env_name
  ```
  
  * deactivate
  ```
  $ conda deactivate
  ```

  * install package list
  ```
  $ conda list
  ```
  
  * environments list
  ```
  $ conda env list
  ```
  