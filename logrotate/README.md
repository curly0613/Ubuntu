# logrotate-tips
logrotate 사용법

### logrotate
* Ubuntu 18.04 기준 default installed

* configuration
  * /etc/logrotate.d/config_name
  * 예제
  ```
  /home/user/path/log/file			// 적용할 log 파일 이름
  {
          su root tbai
          daily					// 일별 log 생성
          rotate 30
          missingok
          notifempty
          dateext				// 파일명 뒤에 날자 붙임
          dateyesterday				// 이전 날자로 생성
          postrotate
              killall -s SIGUSR1 gunicorn	// gunicorn이랑 함께 쓸 때
          endscript
  }
  ```

* logrotate 실행
  ```
  $ sudo logrotate /etc/logrotate.d/config_file
  ```
