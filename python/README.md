# python-tips
python 사용법

### Python
* Install
  * default installed (ubuntu 18.04 기준)
  ```
  sudo apt-get install python-dev (2.7)
  ```

  * 3.6 install
  ```
  $ apt install python3.6-dev

  # 3.6 기본 설정 (terminal에서 python 입력 시 default setting)
  $ update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1
  ```

  * pip install
  ```
  $ wget https://bootstrap.pypa.io/get-pip.py
  $ python get-pip.py
  ```

### virtualenv
* Python 가상 라이브러리 환경
* Install
  ```
  sudo apt-get install virtualenv
  ```

* Build
  * env 폴더에 python3.6 버전 환경 build
  ```
  $ virtualenv --python=python3.6 env
  ```

* 환경 활성화
  ```
  $ source /path/to/env/bin/activate
  (env) ... $
  ```

* 비활성화
  ```
  $ deactivate
  ```

### args
* command arguments
  * In code
  ```
  import argparse

  parser = argparse.ArgumentParser()
  parser.add_argument('-args1', type=str, default='A')
  parser.add_argument('-args2', type=int, default=1)
  args = parser.parse_args()
  ...
  # call 'args.args1', 'args.args2'
  ```

  * Run with arguments
  ```
  $ python test.py -args1 A -args2 0
  ```

### flask


### gunicorn


