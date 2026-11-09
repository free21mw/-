# Velog → GitHub 자동 백업 실습 프로젝트

Velog의 공개 RSS 피드를 읽어 게시글을 Markdown 파일로 저장하고, GitHub Actions로 매일 자동 실행하는 교육용 프로젝트입니다.

## 1. 준비
- GitHub 계정
- 공개 게시글이 있는 Velog 계정
- GitHub Repository

## 2. 저장소 만들기
GitHub에서 `velog-backup`이라는 새 저장소를 만듭니다. 개인 글 보관 목적이라면 Private를 권장합니다. 이 프로젝트 ZIP의 파일을 저장소 최상위에 업로드합니다.

## 3. Velog ID 설정
`scripts/backup_velog.py` 파일에서 아래 값을 바꿉니다. `@`는 입력하지 않습니다.

```python
VELOG_USERNAME = "your_velog_id"
```

예: `https://velog.io/@myname`이면 `myname`

## 4. Actions 쓰기 권한
저장소의 `Settings → Actions → General → Workflow permissions`에서 `Read and write permissions`를 선택하고 저장합니다. 조직 정책이 쓰기를 제한하면 관리자 설정이 우선합니다.

## 5. 수동 실행
1. 저장소의 `Actions` 탭을 엽니다.
2. `Velog Automatic Backup`을 선택합니다.
3. `Run workflow`를 누릅니다.
4. 성공하면 `velog-posts/` 폴더에서 Markdown 파일을 확인합니다.

## 6. 자동 실행
기본 예약은 매일 UTC 00:00, 한국 시간 오전 9시입니다. GitHub 예약 실행은 지연될 수 있습니다.

## 7. 프로필 연결
- GitHub: `Settings → Public profile → Social accounts`에 Velog 주소 추가
- Velog: 프로필 소개 또는 소셜 링크에 GitHub 주소 추가

로그인 연동과 프로필 링크 등록은 별개입니다.

## 8. 폴더 구조
```text
velog-backup/
├── .github/workflows/velog-backup.yml
├── scripts/backup_velog.py
├── velog-posts/
├── requirements.txt
├── .gitignore
└── README.md
```

## 9. 제한 사항
- 공개 RSS에 포함된 게시글만 수집합니다. 비공개·삭제 게시글은 백업할 수 없습니다.
- RSS가 제공하는 게시글 범위에 한계가 있어 과거 모든 글의 수집을 보장하지 않습니다.
- 본문을 Markdown으로 변환하므로 원본 HTML과 완전히 같지 않을 수 있습니다.
- 이미지 파일 자체를 다운로드하지 않습니다. 이미지 URL이 본문에 남을 수 있습니다.
- RSS 형식이나 Velog 접근 정책이 변경되면 코드 수정이 필요할 수 있습니다.

## 10. 실습 과제
1. Velog ID를 설정합니다.
2. Actions에서 수동 실행합니다.
3. `velog-posts/`에 파일이 생성됐는지 확인합니다.
4. Velog에 새 공개 글을 작성합니다.
5. Actions를 다시 실행해 새 글이 추가되는지 확인합니다.
6. 양쪽 프로필에 서로의 링크를 등록합니다.
