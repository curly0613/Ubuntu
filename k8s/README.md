# 사내망 쿠버네티스 구축 및 운영

### 쿠버플로우 Jupyter Notebook 작업환경을 현재 상태를 그대로 Image로 저장하고 다시 불러오는 방법

- nerdctl 활용
  - docoker와 비슷하게 동자갛지만 containerd와 직접 통신 (kubernetes image, container에 접근 가능)
  - k8s 서버에 nerdctl 설치 (바이너리 파일만 옮겨서 실행)
  - docker 명령어와 거의 비슷하다.
  - ```
    $ sudo ./nerdctl --address=/run/k3s/containerd/containerd.sock --namespace k8s.io ps -a | grep <pod_name>
    // --address, --namespace : 현재 동작 중인 kubernetes cluster와 연결
    ```
  - 동작 중인 컨테이너를 이미지로 commit
  - ```
    sudo ./nerdctl --address=/run/k3s/containerd/containerd.sock --namespace k8s.io commit <container_id> <create_image_name>
    ```
  - harbor repository에 이미지 등록
  - ```
    sudo ./nerdctl --address=/run/k3s/containerd/containerd.sock --namespace k8s.io push <docker_hub_url> --insecure-registry
    ```
- Kuberflow에 새 개발환경 등록
  - Docker Image 설정을 Custom Image로 habor repository url 작성
  - Workspace Volumn을 기존에 생성한 volumn과 연동 (Attach existing volumn)

---
### Docker 이미지를 활용한 서비스 실행
- example wiki-js
- 외부망에서 docker image 구축
  - wiki-js
  - postgresql
- docker image habor 업로드
- yaml file 생성 및 apply
- ```
  apiVersion : v1
  kind: List
  items:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: wiki-js
    - apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: wiki-js
        namespace: wiki-js
        labels:
          app: wiki--js
      spec:
        nodeName: storage1
        containers:
          - name: postgresdb
            image: <docker_hub_image_url>
            imagePullPolicy: Always
            ports:
              - containerPort: 5432
            env:
              - name: POSTGRES_DB
                value: wiki
              - name: POSTGRES_PASSWORD
                value: wikijsrocks
              - name: POSTGRES_USER
                value: wikijs
              volumeMounts:
                - name: postgres-data
                  mountPath: /var/lib/postgresql/data
          - name: wiki-js
            image: <docker_hub_image_url>
            imagePullPolicy: Always
            ports:
              - containerPort: 3000
          volumes:
            - name: postgres-data
              hostPath:
                path: /home/wiki/postgres-data
    - apiVersion: v1
      kind: Service
      metadata:
        name: wiki-js
        namespace: wiki-js
        lables:
          app: wiki-js
      spec:
        type: NodePort
        ports:
          - port: 3000
            protocol: TCP
            name: http
        selector:
          app: wiki-js
  ```
- Issue
  - DB connect failed
    - 해결 : wiki-js image 안의 config.yml의 db host 설정 변경(db > 127.0.01 => localhost)
  - DB query 실패
    - 해결 : postgreql container image 초기화 (캐시 이미지 활용 x)
- System reboot 후 확인사항
  - nvidia driver(버전 확인), cuda, docker, nvidia-docker 설치 확인
  - 방화벽 확인(ufw)
  - Iptable 확인
  - 특정 pod에 문제가 있는 경우 대부분 할당 노드 변경으로 인한 storage 문제가 대부분(localpath 활용 시)
