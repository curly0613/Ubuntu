# mongoDB-tips
mongoDB 사용법

### 바로가기
* [mongoDB](#mongo)
* [pymongo](#pymongo)

### <a name="mongo">mongoDB</a>
* 설치
  ```
  sudo apt-get install mongodb
  ```

* configuration
  * /etc/mongodb.conf
    ```
    - 외부 접속 허용
    ...
    line 11
    #bind_ip = 127.0.0.1 수정 전
    bind_ip = 0.0.0.0
    ...

    - 인증 설정
    line 22
    auth = true
    ...

    저장 후 재시작
    $ sudo systemctl restart mongodb.service
    ```
  
  * 인증
    ```
    - 사용자 추가
    $ mongo 
    > use db_name
    > db.creatUser({user: 'ID', pwd: 'PASSWORD', roles: [{role: 'userAdminAnyDatabase', db : 'DB_NAME'}, {role : 'root', db : 'admin'}]})

    - 권한 추가
    > db.grantRolesToUser('ID', [{role:'readWrite', 'db':'DB_NAME'}])

    - 계정 권한 접속
    $ mongo -u ID -p PASSWORD --authenticationDatabase admin
    ```
 
  * 조회
    ```
    database
    > show dbs

    collection (database 선택 후에)
    > show collections
    ```

  * 생성
    ```
    > db.col.insert({ ... })  
    ```

  * 삭제
    ```
    - database
    > db.dropDatabase()
  
    - collection
    > db.col.drop()

    - document
    > db.col.delete({ ... })
    ```

  * 인덱스
    ```
    - 생성
      key는 인덱스 적용할 key 이름
      뒤 숫자 1은 오름차순 (-1은 내림차순)
    > db.col.createIndex({'key':1})

    - 확인
    > db.col.getIndexes()

    - 삭제
    > db.col.dropIndexes()
    ```

### <a name="pymongo">pymongo</a>
* python에서 사용하는 mongoDB library

* 설치
  ```
  $ pip install pymongo
  ```

* 사용법
  - package load & database connect
    ```
    from pymongo import MongoClient 
    
    client = MongoClient()
    db = db.test.test
    ```
  - 수정
    ```
    db.find_one_and_update({'key_1': value_1 }, {'$set' : {'key_2': new_value_2}})

    # list append
    db.find_one_and_update({'key_1': value_1 }, {'$push' : {'key_2': new_value_2}})

    # extend
    db.find_one_and_update({'key_1': value_1 }, {'$push' : {'key_2': {'$each': new_list}}})

    # list delete
    db.find_one_and_update({'key_1': value_1 }, {'$pull' : {'key_2': value_2}})

    # list delete 여러개 contion
    db.find_one_and_update({'key_1': value_1 }, {'$pull' : {'key_2': {'$in' : [value_2, value_3]}})

    # one(0) of inner list delete
    db.find_one_and_update({'key_1': value_1 }, {'$pull' : {'key_2.0.key_3': value_2}})

    # all of inner list delete (multi : 하나만 삭제하지 않고 모두 삭제)
    db.find_one_and_update({'key_1': value_1 }, {'$pull' : {'key_2.$[].key_3': value_2}}, multi=True)

    # 여러 조건을 동시에 적용 가능
    db.find_one_and_update({'key':value}, {'$push':{'key_2':value_2}}, {'$set':{'key_3':value_3})
    ```