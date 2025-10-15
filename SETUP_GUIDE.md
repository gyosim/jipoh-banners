# GitHub Repository 설정 가이드

이 로컬 repository를 GitHub에 업로드하는 방법입니다.

## 📋 준비사항

- GitHub 계정
- Git 설치 완료
- 이 repository가 이미 로컬에 생성됨 ✅

## 🚀 GitHub에 업로드하기

### Step 1: GitHub에서 새 Repository 생성

1. [GitHub](https://github.com)에 로그인
2. 우측 상단 **+** 버튼 클릭 → **New repository** 선택
3. Repository 설정:
   - **Repository name**: `jipoh-banners`
   - **Description**: "JipOh app banner management repository"
   - **Public** 선택 ⚠️ (중요: CDN 접근을 위해 Public 필수)
   - **Initialize this repository with** 체크 해제 (이미 로컬에 있음)
4. **Create repository** 클릭

### Step 2: 로컬 Repository를 GitHub에 연결

터미널에서 다음 명령어 실행:

```bash
cd /Users/kimjungyo/Desktop/gyosim-develop/jipoh-banners

# GitHub repository와 연결 (YOUR_USERNAME을 실제 GitHub username으로 변경)
git remote add origin https://github.com/YOUR_USERNAME/jipoh-banners.git

# 기본 브랜치 이름 확인/변경 (GitHub는 main 사용)
git branch -M main

# GitHub에 푸시
git push -u origin main
```

### Step 3: GitHub에서 확인

1. GitHub repository 페이지 새로고침
2. 파일들이 업로드되었는지 확인:
   - ✅ README.md
   - ✅ banners.json
   - ✅ images/
   - ✅ CHANGELOG.md
   - ✅ .gitignore

### Step 4: jsDelivr CDN URL 확인

브라우저에서 다음 URL을 열어 배너 JSON이 잘 보이는지 확인:

```
https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/banners.json
```

⚠️ **YOUR_USERNAME을 실제 GitHub username으로 변경하세요!**

예시:
```
https://cdn.jsdelivr.net/gh/jiyumi00/jipoh-banners@main/banners.json
```

## ⚙️ Backend 환경 변수 설정

### jipoh-backend/.env 파일 수정

```bash
cd /Users/kimjungyo/Desktop/gyosim-develop/jipoh/jipoh-backend

# .env 파일에 다음 줄 추가 (YOUR_USERNAME 변경)
echo "GITHUB_BANNER_URL=https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/banners.json" >> .env
```

또는 직접 편집:

```bash
# .env 파일 열기
nano .env

# 맨 아래에 추가
GITHUB_BANNER_URL=https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/banners.json

# 저장 후 종료 (Ctrl+X → Y → Enter)
```

## 🚀 Backend 배포

```bash
cd /Users/kimjungyo/Desktop/gyosim-develop/jipoh/jipoh-backend

# Dev 환경 배포
./deploy.sh dev

# 테스트 OK 후 Production 배포
./deploy.sh prod
```

## ✅ 테스트

### 1. API 테스트

```bash
# Dev 환경
curl https://YOUR_DEV_API_URL/banners

# 예상 응답:
# {
#   "success": true,
#   "message": "배너 목록을 성공적으로 조회했습니다",
#   "data": {
#     "banners": [...],
#     "total_count": 2
#   }
# }
```

### 2. 앱에서 확인

- JipOh 앱 실행
- 홈 화면에서 배너 2개 표시 확인

## 📝 배너 업데이트 방법

### GitHub Web UI 사용 (가장 쉬움)

1. GitHub에서 `jipoh-banners` repository 이동
2. `banners.json` 파일 클릭
3. 연필 아이콘 (Edit this file) 클릭
4. JSON 편집
5. 하단 "Commit changes" 클릭
6. **5분 이내 앱에 자동 반영!** ✨

### 로컬에서 수정 후 Push

```bash
cd /Users/kimjungyo/Desktop/gyosim-develop/jipoh-banners

# banners.json 편집
nano banners.json

# Git commit & push
git add banners.json
git commit -m "Update banner: 새 배너 추가"
git push origin main
```

## 🎨 이미지 업로드

### GitHub Web UI 사용

1. `images/` 폴더로 이동
2. "Add file" → "Upload files" 클릭
3. 이미지 파일 드래그앤드롭
4. "Commit changes" 클릭
5. 이미지 URL:
   ```
   https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/images/파일명.jpg
   ```

### 로컬에서 업로드

```bash
cd /Users/kimjungyo/Desktop/gyosim-develop/jipoh-banners

# 이미지 파일을 images/ 폴더에 복사
cp ~/Downloads/my-banner.jpg images/

# Git commit & push
git add images/my-banner.jpg
git commit -m "Add new banner image: my-banner.jpg"
git push origin main
```

## 🔒 보안 체크리스트

- [ ] Repository가 **Public**으로 설정됨 (CDN 접근 필수)
- [ ] `.env` 파일은 절대 커밋하지 않음 (이미 .gitignore에 포함됨)
- [ ] 민감한 정보(API 키 등)를 banners.json에 포함하지 않음
- [ ] 이미지 파일 크기 확인 (100KB 이하 권장)

## ❓ 문제 해결

### "Permission denied" 에러

```bash
# SSH 키 설정 필요
ssh-keygen -t ed25519 -C "your_email@example.com"
# GitHub Settings → SSH and GPG keys에 등록
```

또는 HTTPS 사용 시:

```bash
# GitHub Personal Access Token 필요
# Settings → Developer settings → Personal access tokens에서 생성
```

### "Repository not found" 에러

- GitHub username 확인
- Repository 이름이 정확한지 확인 (`jipoh-banners`)
- Repository가 Public인지 확인

### jsDelivr에서 404 에러

- 5분 기다려보기 (CDN 캐시 생성 시간)
- GitHub에 파일이 정상적으로 푸시되었는지 확인
- URL 오타 확인

## 🎉 완료!

이제 GitHub Web UI에서 배너를 쉽게 관리할 수 있습니다!

---

**다음 단계**: Backend를 배포하고 앱에서 배너가 잘 표시되는지 확인하세요.
