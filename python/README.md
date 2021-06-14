# python-tips
python 사용법

### Python
* Install
  * default installed (ubuntu 18.04 기준)
  ```
  $ sudo apt-get install python-dev (2.7)
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
  
  만약 에러 있으면,
  $ sudo apt-get install python-distutils
  ```

### virtualenv
* Python 가상 라이브러리 환경
* Install
  ```
  $ sudo apt-get install virtualenv
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

### import packages from files
* libs 폴더 참조
```
import sys
sys.path.append('./libs')

import 'PACKAGE_NAME'
```

* libs 폴더에 library 설치
```
$ pip install --system -r requirements.txt -t ./libs/
```

### args
* 비교적 간단한 방법
  * code
  ```
  import sys

  args1 = sys.argv[1]
  args2 = sys.argv[2]
  ```
  
  * Run with arguments (only string)
  ```
  $ python test.py A B
  ```

* use argparse
  * code
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
* Install
  ```
  $ pip install flask flask-socketio
  ```
  * usage
    * 주로 웹페이지 구현에 활용
    ```
    # app.py
    from flask import Flask, render_template, request
    from flask_socketio import SocketIO, send

    app = Flask(__name__)
    app.secret_key = "mysecretkey"

    socket_io = SocketIO(app)

    @app.route('/')
    def root():
      return render_template('demo_home.html', host_url=request.host_url)
    
    @socket_io.on("message")
    def reply(message):
      to_client = { 'input' : message }
      send(to_client)

    if __name__ == '__main__':
      socket_io.run(app, debug=True, host='IP_ADDRESS', port=PORT)
    ```

  * flask restful
    * REST API 용
    * install
      ```
      $ pip install flask flask-restful
      ```
    * usage
      ```
      from flask import Flask, request
      from flask_restful import Resource, Api
    
      app = Flask(__name__)
      api = Api(app)

      class WELCOME(Resource) :
      '''
      Welcome and return HELLO WORLD!
      '''

      def post(self) :
          input_json = request.json.copy()
          return { 'input' : input_json, 'output' : 'HELLO, WORLD!!' }

      api.add_resource(WELCOME, '/welcome')

      if __name__ == '__main__':
        app.run(host='IP_ADDRESS', port=PORT, debug=True, use_reloader=True)
      ```

  * flask monitoring dashboard
  ```
  $ pip install flask-monitoringdashboard
  ```

### gunicorn
* Install
  ```
  $ pip install gunicorn
  ```

* Run
  * 최적의 WORKER 수 : (2 x *$NUM_OF_CORES*) + 1
  ```
  $ gunicorn <FLASK_CODE_NAME>:app -w <NUM_OF_WORKERS> -k gevent -b 0.0.0.0:<PORT_NUM> --log-file <LOG_FILE> --log-level INFO --reload
  ```
  * Log setting
  ```
  import logging
  
  ...
  
  gunicorn_error_logger = logging.getLogger('gunicorn.error')
  app.logger.handlers = gunicorn_error_logger.handlers
  app.logger.setLevel(logging.INFO)
  
  ...
  
  app.logger.info("LOG_MESSAGE)
  ```
