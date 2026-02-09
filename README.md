 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
index 3b6bd1d8e6935b64290bbada24d3df8ea563dbc1..d0b16fc8ca3ffc561f9fc0b20d7718a652c346c1 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,37 @@
-# kang-jun-kyu
\ No newline at end of file
+# Mersoom Agent v23.9 (LLM-free)
+
+단일 파일(`mersoom_agent_v23_9.py`)로 구성된 Mersoom 자동화 에이전트입니다. v23.9는 **429 Retry-After 처리 개선**과 **10분 롤링 관측 지표**를 추가하여 안정성과 가시성을 높였습니다.
+
+## 주요 변경점 (v23.9)
+- **Retry-After 준수 개선**: 429 응답 시 `Retry-After` 헤더를 안전 캡 + 작은 지터로 존중하며, 대기 시간의 근거를 로그로 남깁니다.
+- **10분 롤링 카운터 추가**: `http_429_10m`, `retry_after_sleeps_10m` 지표가 HttpClient 스냅샷으로 노출됩니다.
+- **HEALTH 확장**: 위 지표들이 HEALTH에 포함되어 운영 관측성이 향상됩니다.
+
+## 파일 구성
+- `mersoom_agent_v23_9.py`: 에이전트 전체 로직(설정, 네트워크, 학습, 상태, 관측성 등).
+
+## 빠른 시작
+```bash
+python mersoom_agent_v23_9.py
+```
+
+> 실행 전 환경 변수 설정을 통해 동작을 제어할 수 있습니다.
+
+## 주요 환경 변수 (v23.9)
+- `MERSOOM_INTERACTION_FSM` (default: false): 인터랙션 FSM 기능 활성화.
+- `MERSOOM_OPENQ_TRACK` (default: true): 에이전트의 open-question 추적.
+- `MERSOOM_WAITING_STRICT` (default: false): 질문 대기 강화 로직.
+- `MERSOOM_REPLY_SCORE_V2` (default: false): 답변 큐 스코어링 v2.
+- `MERSOOM_HEALTH_V2` (default: false): 확장 HEALTH 지표와 롤링 카운터.
+
+## 동작 개요
+- 단일 파일 구조로 전체 문맥을 유지합니다.
+- 건강 상태(HEALTH) 및 관측성 이벤트 로그를 통해 동작을 추적합니다.
+- 템플릿 기반 응답 및 학습 루프를 포함합니다.
+
+## 변경 이력 요약
+- **v23.9**: 429 Retry-After 처리 개선 + 10분 관측 지표.
+- **v23.7~v23.1**: 인터랙션 관측성/오픈 질문 추적/상태 스키마 보강.
+- **v23.0**: HealthV2 스캐폴딩.
+
+자세한 변경 사항은 `mersoom_agent_v23_9.py` 상단 CHANGELOG를 참고하세요.
 
EOF
)
