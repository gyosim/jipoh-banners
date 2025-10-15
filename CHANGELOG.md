# Changelog

배너 변경 이력을 기록합니다.

## [1.0.0] - 2024-10-15

### Added
- 초기 배너 저장소 생성
- 샘플 배너 2개 추가
  - `banner-001`: 수학 실력 향상 이벤트
  - `banner-002`: 새로운 기능 출시

### Notes
- DynamoDB에서 GitHub으로 마이그레이션 완료
- jsDelivr CDN을 통한 무료 호스팅

---

## 변경 기록 작성 가이드

새 배너를 추가하거나 수정할 때마다 아래 형식으로 기록하세요:

```markdown
## [버전] - YYYY-MM-DD

### Added (추가)
- 새로운 배너 설명

### Changed (변경)
- 기존 배너 수정 내용

### Removed (제거)
- 제거된 배너

### Notes (비고)
- 기타 참고사항
```

### 예시

```markdown
## [1.1.0] - 2024-12-01

### Added
- `banner-winter-event`: 겨울 방학 특별 이벤트 배너 추가

### Changed
- `banner-001`: 이미지 URL 업데이트 (placeholder → 실제 이미지)
- `banner-002`: 종료일 연장 (2025-06-30 → 2025-12-31)

### Removed
- `banner-old-promo`: 만료된 프로모션 배너 제거

### Notes
- 겨울 방학 이벤트는 2월 말까지 진행
```
