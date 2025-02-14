# 🚀 GitHub Actions을 사용하여 Render 서버 자동 Ping 보내기

## 📌 목표
Render.com의 무료 플랜에서는 **Cold Start(콜드 스타트)** 문제가 발생할 수 있습니다.  
서버가 일정 시간 동안 요청이 없으면 절전 상태로 들어가고, 다시 시작할 때 속도가 느려지는 문제가 발생합니다.  

✅ **이 문제를 해결하기 위해 GitHub Actions을 사용하여 10분마다 Render 서버를 깨우는 방법을 설정합니다.**  
✅ **GitHub Actions은 무료로 실행되므로 유지 비용이 없습니다.**  

---

## 🔹 1. GitHub Actions이란?
- **GitHub Actions**는 **GitHub에서 제공하는 자동화 도구**입니다.
- **정해진 시간마다 특정 작업을 실행**할 수 있습니다. (예: Render 서버에 Ping 보내기)
- **무료 티어 제공** (월 2,000분 사용 가능 → 충분함)

---

## 🔹 2. GitHub Actions 설정하기
이제 GitHub Actions을 사용해서 **Render 서버가 절전 모드로 들어가지 않도록 자동 Ping을 보내는 작업을 설정**할 것입니다.  
👉 **최종 목표:** Render 서버가 절전 모드로 들어가지 않도록 **10분마다 자동으로 Ping을 보냄.**

---

## 📌 1단계: GitHub 저장소 만들기
1. **GitHub 웹사이트에 접속** → [GitHub](https://github.com)
2. **로그인 후 새 저장소(Repository) 생성**
   - 🔹 `New Repository` 버튼 클릭
   - 🔹 **Repository Name:** `render-ping`
   - 🔹 **공개(Private/Public) 선택:** 아무거나 가능
   - 🔹 **초기화 설정**
     - ✅ `Add a README file` 체크
   - **마지막으로 `Create Repository` 클릭**

---

## 📌 2단계: GitHub Actions 설정하기

### 1️⃣ Actions 탭으로 이동
1. GitHub 저장소에서 **`Actions`** 탭 클릭
2. **"New Workflow" 또는 "Set up a workflow yourself"** 버튼 클릭
3. 새 파일 편집 화면이 나타남

---

## 📌 3단계: Actions YAML 파일 만들기
이제 GitHub Actions 파일을 직접 만들겠습니다.

### 1️⃣ `.github/workflows/ping.yml` 파일 만들기
1. GitHub 저장소에서 **"Code"** 탭으로 이동
2. **"Add File"** 클릭 → **"Create new file"** 선택
3. **파일명 입력:** `.github/workflows/ping.yml`
   - 📌 `.github/workflows/` 폴더 안에 넣어야 GitHub Actions이 실행됩니다.

### 2️⃣ Actions 내용 입력 (10분마다 Render 서버 깨우기)
아래 코드를 **파일에 복사 & 붙여넣기** 합니다.

```yaml
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
```
설명:
- cron: "*/10 * * * *" → 10분마다 실행됨
- curl -s https://fastapi-render-m0ga.onrender.com/ > /dev/null
- Render 서버에 HTTP 요청을 보내서 깨움
- /dev/null → 불필요한 출력 제거

## 📌 4단계: GitHub Actions 파일 저장
1. 파일 하단에서 "Commit new file" 클릭
- Commit message: "Add GitHub Actions for Render server ping"
- ✅ Commit directly to the main branch 체크
2. 저장이 완료되면 자동으로 Actions이 실행됩니다.

## 📌 5단계: GitHub Actions 실행 확인
1. GitHub 저장소에서 "Actions" 탭 클릭
2. 새로운 워크플로우 실행 상태 확인
- "Keep Render Server Awake" 작업이 정상적으로 실행되었는지 확인
3. 실행 로그에서 "Send Ping Request" 가 실행된 걸 볼 수 있음.

 ## 🚀 최종 결과
✅ 이제 Render 서버가 절전 모드로 들어가지 않도록 10분마다 자동으로 Ping을 보냄.
✅ GitHub Actions이 무료로 실행되므로 유지 비용이 없음.
✅ 이제 별도의 추가 작업 없이 서버가 Cold Start 문제 없이 유지됨.


  
  



