# tmux-tips
tmux 사용법

### tmux 설치
* ubuntu 18.04 기준
  ```
  $ sudo apt-get update
  $ sudo apt-get install tmux
  ```

### tmux 사용법
* tmux 2.6 기준
  * tmux 실행 전 (커맨드 라인)
    - tmux 실행
      ```
      $ tmux
      ```
    - tmux 목록 확인
      ```
      $ tmux ls
      0: 1 windows (created Tue Dec  1 15:55:39 2020) [204x59]
      1: 1 windows (created Tue Dec  1 15:56:36 2020) [204x59]
      3: 1 windows (created Wed Dec  2 11:23:17 2020) [204x59]
      ```
    - 실행 중인 tmux에서 작업 시작
      ```
      $ tmux attach -t <num>
      ```

  * tmux 실행 후
    - 모든 커맨드는 ctrl+b 를 입력하고 적용
    - tmux 탈출
      ```
      (ctrl+b) d
      ```
    - tmux 가로 화면 분할
      ```
      (ctrl+b) "
      ```
    - tmux 세로 화면 분할
      ```
      (ctrl+b) %
      ```
    - tmux 분할 화면 간 이동
      ```
      (ctrl+b) <화살표>
      ```
    - tmux 분할 화면 크기 조정
      ```
      (ctrl+b) 누른 상태에서 <화살표>
      ```
    - tmux 분할 이동
      ```
      (ctrl+b) '[' or ']'
      ```
    - tmux 화면 내 스크롤 (종료는 Esc)
      ```
      (ctrl+b) 'pageUp' or 'pageDown'
      ```
    - tmux 종료 (tmux 내 커맨드 라인에서)
      ```
      $ exit
      ``` 
