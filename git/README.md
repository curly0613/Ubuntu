# git-tips
git 사용법

### git bash 터미널 계정
* 현재 계정 확인
  ```
  $ git config user.name
  $ git config user.email
  ```

* 계정 변경
  ```
  $ git config --global user.name <user_id>
  $ git config --global user.email <user_email_address>
  ```

* Repository 추가
  ```
  $ git clone <git_url>
  or
  $ git remote add origin <git_url>
  ```

* Repository 업로드
  ```
  $ git add <file_or_folder>
  $ git commit -m "COMMIT_MESSAGES"
  $ git push -u origin master
  ```



