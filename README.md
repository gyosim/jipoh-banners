# JipOh Banners Repository

집오(JipOh) 앱의 배너를 관리하는 저장소입니다.

## 📁 구조

```
jipoh-banners/
├── README.md           # 이 파일
├── banners.json        # 배너 메타데이터 (메인 파일)
└── images/             # 배너 이미지들
    ├── banner-math-event.jpg
    ├── banner-summer-sale.jpg
    └── ...
```

## 🎯 사용 방법

### 1. 배너 추가/수정

1. GitHub Web UI에서 `banners.json` 파일 열기
2. 연필 아이콘 (Edit) 클릭
3. JSON 편집
4. "Commit changes" 클릭
5. **5분 이내 앱에 자동 반영됨** (jsDelivr CDN 캐시)

### 2. 이미지 업로드

1. `images/` 폴더로 이동
2. "Add file" > "Upload files" 클릭
3. 이미지 파일 드래그앤드롭
4. Commit
5. 이미지 URL 복사:
   ```
   https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/images/파일명.jpg
   ```

### 3. 배너 활성화/비활성화

**활성화:**
```json
{
  "status": "active",
  "start_date": "2024-01-01T00:00:00Z",
  "end_date": "2025-12-31T23:59:59Z"
}
```

**비활성화:**
```json
{
  "status": "inactive"
}
```

## 📋 배너 JSON 스키마

```json
{
  "version": "1.0",
  "last_updated": "2024-10-15T10:00:00Z",
  "banners": [
    {
      "banner_id": "unique-id",
      "title": "배너 제목",
      "description": "배너 설명",
      "image_url": "https://cdn.jsdelivr.net/gh/USER/jipoh-banners@main/images/image.jpg",
      "target_url": "https://example.com/event",
      "priority": 1,
      "status": "active",
      "start_date": "2024-01-01T00:00:00Z",
      "end_date": "2025-12-31T23:59:59Z"
    }
  ]
}
```

### 필드 설명

| 필드 | 타입 | 설명 |
|------|------|------|
| `banner_id` | string | 배너 고유 ID (예: `banner-001`) |
| `title` | string | 배너 제목 |
| `description` | string | 배너 설명 (선택사항) |
| `image_url` | string | 이미지 URL (jsDelivr CDN 권장) |
| `target_url` | string | 클릭 시 이동할 URL |
| `priority` | number | 우선순위 (낮을수록 먼저 표시) |
| `status` | string | `active` 또는 `inactive` |
| `start_date` | string | 노출 시작일 (ISO 8601 형식) |
| `end_date` | string | 노출 종료일 (ISO 8601 형식) |

## 🔗 URL 확인

배너 JSON이 잘 배포되었는지 확인:

```
https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/banners.json
```

## ⚙️ 백엔드 설정

Backend `.env` 파일에 다음 추가:

```bash
GITHUB_BANNER_URL=https://cdn.jsdelivr.net/gh/YOUR_USERNAME/jipoh-banners@main/banners.json
```

## 📊 배너 예시

### 이벤트 배너
```json
{
  "banner_id": "event-2024-winter",
  "title": "겨울 방학 특별 이벤트",
  "description": "매일 문제 풀고 선물 받자!",
  "image_url": "https://cdn.jsdelivr.net/gh/USER/jipoh-banners@main/images/winter-event.jpg",
  "target_url": "https://jipoh.com/events/winter-2024",
  "priority": 1,
  "status": "active",
  "start_date": "2024-12-01T00:00:00Z",
  "end_date": "2025-02-28T23:59:59Z"
}
```

### 기능 안내 배너
```json
{
  "banner_id": "feature-review-system",
  "title": "복습 알림 기능 출시!",
  "description": "잊기 전에 복습하세요",
  "image_url": "https://cdn.jsdelivr.net/gh/USER/jipoh-banners@main/images/review-feature.jpg",
  "target_url": "https://jipoh.com/features/review",
  "priority": 2,
  "status": "active",
  "start_date": "2024-10-01T00:00:00Z",
  "end_date": "2025-12-31T23:59:59Z"
}
```

## 🎨 이미지 가이드라인

### 권장 사항
- **크기**: 400 x 120px (3.33:1 비율)
- **파일 형식**: JPG 또는 PNG
- **파일 크기**: 100KB 이하 (최적화 필수)
- **해상도**: @2x 이미지 권장 (800 x 240px)

### 디자인 팁
- 텍스트는 이미지에 포함 (JSON title은 접근성용)
- 모바일에서 가독성 고려
- JipOh 브랜드 컬러 사용 권장 (#0061f8)

## ⚠️ 주의사항

### JSON 문법 검증
- 배너 추가/수정 전 [JSONLint](https://jsonlint.com/)에서 검증
- 쉼표 빠짐, 따옴표 누락 주의

### 캐시 관리
- jsDelivr CDN은 최대 7일 캐싱
- 즉시 업데이트 필요시 버전 태그 사용:
  ```
  https://cdn.jsdelivr.net/gh/USER/jipoh-banners@v1.0.1/banners.json
  ```

### Repository 설정
- **Public Repository**로 유지 (CDN 접근 필요)
- 민감한 정보 포함 금지

## 🔍 문제 해결

### 배너가 앱에 안 보일 때
1. JSON 문법 오류 확인
2. `status: "active"` 확인
3. `start_date`, `end_date` 확인
4. 브라우저에서 JSON URL 직접 확인
5. 5분 기다려보기 (CDN 캐시)

### 이미지가 안 보일 때
1. 이미지 URL 확인 (브라우저에서 직접 열기)
2. 파일 확장자 대소문자 확인 (.jpg vs .JPG)
3. GitHub에 이미지 업로드 확인

## 📞 연락처

문제가 있거나 도움이 필요하면:
- GitHub Issues 생성
- Backend 담당자에게 문의

---

**Last Updated**: 2024-10-15
**Managed by**: JipOh Team
