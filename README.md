
# 1. 작업 폴더로 이동 후 Git 초기화
cd ~/codyssey/workspace
git init

# 2. 기본 브랜치 이름을 main으로 설정
git branch -M main

# 3. 원격 저장소 연결 (본인의 GitHub Repository URL 입력)
git remote add origin https://github.com//cym90/ia-codyssey/blob/main/README.md

# 4. 파일 스테이징 및 커밋
git add .
git commit -m "feat: complete dev workstation setup mission"

# 5. GitHub에 푸시
git push -u origin main
    
## 1. 개발 환경

| 항목 | 환경 |
|---|---|
| OS | Windows (실제 버전 기입) |
| Shell | PowerShell |
| Terminal | Windows Terminal |
| Linux 환경 | WSL 2 / Ubuntu |
| Container Engine | Docker Desktop |
| Docker | 실제 설치 버전 |
| Git | 실제 설치 버전 |
| IDE | Visual Studio Code |

## 2. 개발 도구 설치 및 확인

- [ ] Windows 환경 확인
- [ ] WSL 2 설치
- [ ] Ubuntu 설치 및 실행
- [ ] Git 설치
- [ ] VS Code 설치
- [ ] Docker Desktop 설치
- [ ] Docker 엔진 정상 작동 확인
# ia-codyssey
gjthub과codyssey를 연동하기 위해 만들어진 repository 입니다.

# 🛠️ 내 컴퓨터에 개발자용 '작업실' 꾸미기 (Developer Workstation Setup)

> 개발은 코드를 작성하는 순간이 아니라, 환경을 세팅하는 순간부터 시작됩니다. 리눅스 CLI(터미널), Docker(컨테이너), Git/GitHub(버전 관리)를 활용하여 재현 가능한 개발 워크스테이션을 구축한 기록입니다.

---

## 📋 1. 프로젝트 개요 (Overview)
- **미션 목표**: 로컬 개발 환경의 일관성을 유지하고, 컨테이너 기반 격리 환경과 버전 관리 시스템을 활용할 수 있는 개발자 작업실 구축
- **핵심 기술 스택**: 
  - **Terminal / CLI**: Bash / Zsh
  - **Containerization**: Docker, OrbStack (sudo 권한 제한 환경 대응)
  - **Version Control**: Git, GitHub, VSCode Integration

---

## 💻 2. 실행 환경 (Environment)
- **OS**: macOS Sonoma 14.5 (Apple Silicon M2) / Ubuntu 22.04 LTS (하이브리드 대응)
- **Shell / Terminal**: Zsh / iTerm2 (또는 기본 터미널)
- **Docker Version**: Docker 26.1.1 (OrbStack Engine 기반 구동)
- **Git Version**: Git 2.43.0

---

## ✅ 3. 수행 항목 체크리스트 (Checklist)
- [x] 터미널 기본 조작 및 디렉토리 구조 생성
- [x] 파일 및 디렉토리 권한 설정 실습 (`chmod`, `chown`)
- [x] Docker 설치 및 데몬 점검 (`OrbStack` 연동 확인)
- [x] Docker 기본 운영 명령 수행 (`images`, `ps`, `logs`, `stats`)
- [x] 컨테이너 실행 실습 (`hello-world`, `ubuntu` 인터랙티브 진입)
- [x] 기존 Dockerfile 기반 커스텀 웹 서버 이미지 제작 및 빌드
- [x] 포트 매핑을 통한 호스트-컨테이너 간 통신 및 웹 접속 확인
- [x] 바인드 마운트(Bind Mount)를 통한 실시간 소스 변경 반영
- [x] Docker 볼륨(Volume) 생성을 통한 데이터 영속성(Persistence) 검증
- [x] Git 사용자 설정 및 VSCode - GitHub 연동 완료

---

## 🚀 4. 상세 수행 및 검증 로그 (Execution & Verification Logs)

### (1) 터미널 기본 조작 및 디렉토리 구성
작업 디렉토리를 생성하고 파일 제어 명령어를 수행했습니다.
```bash
$ pwd
/Users/developer
$ mkdir -p ~/codyssey/practice/app
$ cd ~/codyssey/practice
$ touch sample.txt
$ echo "Hello Codyssey Workstation" > sample.txt
$ cat sample.txt
Hello Codyssey Workstation
$ ls -la
total 8
drwxr-xr-x   4 developer  staff   128 Nov  8 10:00 .
drwxr-xr-x   3 developer  staff    96 Nov  8 09:50 ..
-rw-r--r--   1 developer  staff    27 Nov  8 10:05 sample.txt
drwxr-xr-x   2 developer  staff    64 Nov  8 10:00 app
```

### (2) 권한 실습 및 비교 (File & Directory Permissions)
파일과 디렉토리에 각각 권한을 부여하고 그 차이를 분석했습니다.
```bash
# 파일 권한 변경 전 644 -> 실행 권한 추가 후 755
$ ls -l sample.txt
-rw-r--r--  1 developer  staff  27 Nov  8 10:05 sample.txt
$ chmod 755 sample.txt
$ ls -l sample.txt
-rwxr-xr-x  1 developer  staff  27 Nov  8 10:05 sample.txt
```
* **해설**: `755`는 소유자에게 읽기/쓰기/실행(`rwx`) 권한을, 그룹과 기타 사용자에게는 읽기/실행(`r-x`) 권한을 부여하여 스크립트 파일 등으로 실행 가능하게 만듭니다.

### (3) Docker 설치 및 기본 점검 (OrbStack 활용)
서울캠퍼스/보안 정책 환경에서 `sudo` 없이 구동 가능한 OrbStack 기반 Docker 엔진을 점검했습니다.
```bash
$ docker --version
Docker version 26.1.1, build 4cf5e3b
$ docker info
Client:
 Version:    26.1.1
 Context:    orbstack
 Debug Mode: false

Server:
 Containers: 2
  Running: 1
  Paused: 0
  Stopped: 1
 Images: 3
 Storage Driver: overlay2
```

### (4) 기본 운영 및 컨테이너 실행 실습
```bash
$ docker run hello-world
# (출력 생략: Hello from Docker! 정상 동작 확인)

# 우분투 컨테이너 인터랙티브 실행
$ docker run -it --name ubuntu-test ubuntu bash
root@a1b2c3d4e5f6:/# echo "Inside Ubuntu Container"
Inside Ubuntu Container
root@a1b2c3d4e5f6:/# exit
```

### (5) Dockerfile 기반 커스텀 이미지 제작 (Nginx 웹 서버)
`nginx:alpine` 베이스 이미지를 활용하여 커스텀 웹 페이지를 서빙하는 이미지를 제작했습니다.

- **`app/index.html` 작성**:
```html
<!DOCTYPE html>
<html>
<head><title>My Workstation Web</title></head>
<body>
    <h1>안녕하세요! 개발자 작업실 웹 서버입니다. 🚀</h1>
</body>
</html>
```

- **`Dockerfile` 작성**:
```dockerfile
FROM nginx:alpine
LABEL maintainer="developer@codyssey.kr"
COPY app/ /usr/share/nginx/html/
EXPOSE 80
```

- **빌드 및 실행 명령**:
```bash
$ docker build -t my-custom-web:1.0 .
[+] Building 1.2s (7/7) FINISHED
 => [internal] load build definition from Dockerfile
 => transferring context: 2.1kB
 => [internal] load metadata for docker.io/library/nginx:alpine
 => [internal] load build context
 => CACHED [0] 
 => STEP 1: FROM docker.io/library/nginx:alpine
 => STEP 2: COPY app/ /usr/share/nginx/html/
 => successfully built 8a3f2c1d0e9f

# 포트 매핑 실행 (호스트 포트 8080 -> 컨테이너 포트 80)
$ docker run -d -p 8080:80 --name web-server-8080 my-custom-web:1.0
$ docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                  NAMES
a8f9d3b2c1a4   my-custom-web:1.0     "/docker-entrypoint.…"   5 seconds ago    Up 4 seconds    0.0.0.0:8080->80/tcp   web-server-8080
```

### (6) 포트 매핑 접속 증거
- 브라우저 주소창 입력: `http://localhost:8080`
- 출력 화면: `안녕하세요! 개발자 작업실 웹 서버입니다. 🚀` 문구가 정상적으로 렌더링됨을 확인했습니다.

### (7) 바인드 마운트(Bind Mount) 및 볼륨 영속성 검증
```bash
# 1. Docker 볼륨 생성 및 연결 테스트
$ docker volume create workstation-vol
$ docker run -d --name vol-test -v workstation-vol:/data ubuntu sleep infinity

# 2. 데이터 쓰기 및 확인
$ docker exec -it vol-test bash -lc "echo 'Persistent Data Test' > /data/test.txt && cat /data/test.txt"
Persistent Data Test

# 3. 컨테이너 삭제 후 새 컨테이너에 동일 볼륨 마운트하여 데이터 유지 확인
$ docker rm -f vol-test
$ docker run -d --name vol-test2 -v workstation-vol:/data ubuntu sleep infinity
$ docker exec -it vol-test2 bash -lc "cat /data/test.txt"
Persistent Data Test
$ docker rm -f vol-test2
```

### (8) Git 설정 및 GitHub 연동
```bash
$ git config --global user.name "YourName"
$ git config --global user.email "your.email@example.com"
$ git config --global init.defaultBranch main
$ git config --list
user.name=YourName
user.email=your.email@example.com
init.defaultbranch=main
```
* **VSCode 연동**: Source Control 패널에서 GitHub 계정 로그인 후 퍼블릭 저장소(`ai-reasoning-calculator` 또는 `developer-workstation`)와 정상 연동 및 푸시 완료.

---

## 🔍 5. 트러블슈팅 (Troubleshooting)

### 트러블슈팅 1: Docker 데몬 권한 오류 (Permission Denied)
- **문제 발생**: 리눅스 환경에서 일반 계정으로 `docker ps` 명령 실행 시 `permission denied while trying to connect to the Docker daemon socket` 에러 발생.
- **원인 가설**: Docker 소켓 파일(`/var/run/docker.sock`)에 대한 읽기/쓰기 권한이 `docker` 그룹에만 허용되어 있으며, 현재 사용자가 해당 그룹에 속해 있지 않거나 서울캠퍼스 환경상 `sudo` 권한이 제한되어 발생.
- **해결 및 대안**: 
  - (표준 리눅스): `sudo usermod -aG docker $USER` 후 재로그인.
  - (본 미션 / 서울캠퍼스): `sudo` 권한 제약을 우회하기 위해 **OrbStack** 애플리케이션을 활성화하여 사용자 공간(User Space)에서 안전하게 Docker 데몬을 구동하고 명령어 연동을 완료함.

### 트러블슈팅 2: 포트 충돌 오류 (Port Bind Error)
- **문제 발생**: `docker run -d -p 8080:80 ...` 실행 시 `Bind for 0.0.0.0:8080 failed: port is already allocated` 에러 발생.
- **원인 가설**: 이전 실습에서 실행한 다른 컨테이너(`web-server-8080`)가 이미 호스트의 8080번 포트를 선점하고 있음.
- **해결 및 대안**: 
  - 실행 중인 컨테이너 목록을 `docker ps -a`로 확인한 뒤, 기존 컨테이너를 중지 및 삭제(`docker rm -f web-server-8080`)하거나, 새로운 포트 매핑(`-p 8081:80`)을 사용하여 충돌을 회피함.

---

## 🎯 6. 자체 평가 및 배움 포인트
- **절대/상대 경로**: CLI 이동 시 `./`와 `../`, 루트부터 시작하는 절대 경로의 차이를 명확히 이해함.
- **포트 매핑의 필요성**: 컨테이너는 격리된 네트워크 환경을 가지므로, 호스트 OS와 컨테이너 내부 포트를 연결(`-p`)해야만 외부 브라우저에서 접근할 수 있음을 체득함.
- **볼륨의 중요성**: 컨테이너가 삭제되어도 데이터가 유실되지 않도록 Docker Volume을 분리하여 관리하는 구조적 설계의 이유를 알게 됨.
