# 1. 작업 폴더로 이동 후 Git 초기화
cd ~/codyssey/workspace
git init

# 2. 기본 브랜치 이름을 main으로 설정
git branch -M main

# 3. 원격 저장소 연결 (본인의 GitHub Repository URL 입력)
git remote add origin https://github.com/cym90/ia-codyssey/edit/main/README.md.git

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
