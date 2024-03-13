# 사내망 쿠버네티스 구축 및 운영

## 쿠버플로우에서 Jupyter Notebook으로 작업환경 생성 시 현재 상태를 그대로 Image로 저장하고 다시 불러오는 방법

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
