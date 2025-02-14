# render-ping

📌 1단계: GitHub 저장소 만들기
GitHub 웹사이트에 접속 → GitHub
로그인 후 새 저장소(Repository) 생성
🔹 New Repository 버튼 클릭
🔹 Repository Name: render-ping
🔹 공개(Private/Public) 선택: 아무거나 가능
🔹 초기화 설정
✅ Add a README file 체크
마지막으로 Create Repository 클릭
📌 2단계: GitHub Actions 설정하기
이제 GitHub Actions을 설정할 파일을 만들자!

1️⃣ Actions 탭으로 이동
GitHub 저장소에서 Actions 탭 클릭
"New Workflow" 또는 "Set up a workflow yourself" 버튼 클릭
새 파일 편집 화면이 나타남
📌 3단계: Actions YAML 파일 만들기
이제 GitHub Actions 파일을 직접 만들 거야.

1️⃣ .github/workflows/ping.yml 파일 만들기
GitHub 저장소에서 "Code" 탭으로 이동
"Add File" 클릭 → "Create new file" 선택
파일명 입력: .github/workflows/ping.yml
📌 .github/workflows/ 폴더 안에 넣어야 GitHub Actions이 실행됨.
2️⃣ Actions 내용 입력 (10분마다 Render 서버 깨우기)
아래 코드를 파일에 복사 & 붙여넣기 해줘.

yaml
복사
편집
name: Keep Render Server Awake

on:
  schedule:
    - cron: "*/10 * * * *"  # 10분마다 실행 (크론 스케줄)

jobs:
  ping:
    runs-on: ubuntu-latest
    steps:
      - name: Send Ping Request
        run: curl -s https://fastapi-render-m0ga.onrender.com/ > /dev/null
✅ 설명:

cron: "*/10 * * * *" → 10분마다 실행됨
curl -s https://fastapi-render-m0ga.onrender.com/ > /dev/null
Render 서버에 HTTP 요청을 보내서 깨움
> /dev/null → 불필요한 출력 제거
📌 4단계: GitHub Actions 파일 저장
파일 하단에서 "Commit new file" 클릭
Commit message: "Add GitHub Actions for Render server ping"
✅ Commit directly to the main branch 체크
저장이 완료되면 자동으로 Actions이 실행됨.
📌 5단계: GitHub Actions 실행 확인
GitHub 저장소에서 "Actions" 탭 클릭
새로운 워크플로우 실행 상태 확인
"Keep Render Server Awake" 작업이 정상적으로 실행되었는지 확인
실행 로그에서 "Send Ping Request" 가 실행된 걸 볼 수 있음.
