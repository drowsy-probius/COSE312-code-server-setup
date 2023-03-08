기본으로 주어진 vagrant도 좋은 솔루션이지만 가상머신 설치해야하는 불편함이 있어 도커로 사용할 수 있는 환경을 구축했습니다.

외부에서 접근 가능한 서버에 컨테이너를 구동하는 것을 상정하고 작성했습니다.

컨테이너의 이미지는 vscode를 웹 IDE로 사용할 수 있는 `code-server` 프로그램의 도커 포팅 버전 중 `linuxserver/code-server`를 사용하였습니다.

ocaml 및 관련 설정으로 인하여 컨테이너의 첫 구동 시간이 오래 걸릴 수 있습니다. 내부 볼륨이 삭제되지 않는 한 재시작할 때에는 비교적 빠른 시간 내에 컨테이너가 부팅됩니다.

필요한 것으로 보이는 vscode 익스텐션은 자동으로 설치되도록 구성하였습니다.

컨테이너 내의 쉘은 `bash`를 사용하는 것으로 스크립트가 작성되어 있습니다. 그리고 사용자명이나 UID 등은 `linuxserver/code-server`이미지에서 제공하는 기본 값으로 고정했습니다. 

`bootstrap.sh` 스크립트의 headless 실행을 위하여 `sudo` 요청 시 패스워드 입력을 비활성화했습니다.

# Setup

1. install docker, docker-compose

2. make directory to store files
vscode 파일과 프로젝트 파일이 저장될 폴더를 생성합니다.

3. copy files
`99-setup`, `bootstrap.sh`를 호스트의 적절한 폴더에 복사합니다.

```
예시

/code-server-ocaml
  | - docker-compose.yml
  | - /settings
       | - 99-setup
       | - bootstrap.sh
  | - /workspace
```

4. edit files
개인 설정에 맞게 `docker-compose.yml`파일을 수정합니다.

5. deploy
`docker compose up -d` 명령어를 통하여 컨테이너를 실행합니다.
