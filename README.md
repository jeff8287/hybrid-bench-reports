# hybrid-bench reports

Public HTML reports for the [hybrid-bench](https://github.com/jeff8287/hybrid-bench) research project — Intel Lunar Lake (4P+4E) 하이브리드 CPU 의 pandas 작업 자동 튜닝.

## Reports

| Date | Report | Description |
|------|--------|-------------|
| 2026-05-12 | [**Phase 1 Final**](https://jeff8287.github.io/hybrid-bench-reports/PHASE_1_FINAL_REPORT.html) | Phase 1 종료 — `bpd.auto_ratio.predict_ratio()` API 출시. 32 APIs, K=4 hybrid, LOOCV 81% 통과. |
| 2026-05-12 | [Stage 8 Validation](https://jeff8287.github.io/hybrid-bench-reports/STAGE_8_VALIDATION_REPORT.html) | predict_ratio() overhead < 0.003%, realized speedup 4.79x mean, 87% APIs ≥ 3x. |
| 2026-05-13 | [Stage 4 SF=5 Partial](https://jeff8287.github.io/hybrid-bench-reports/STAGE_4_SF5_PARTIAL.html) | SF=5 contention grid partial (8/32 workloads). filter, merge_singkey scaling 악화 (cache pressure), column_arith/sort 향상. |
| 2026-05-12 | [Phase A Public Report](https://jeff8287.github.io/hybrid-bench-reports/PHASE_A_PUBLIC_REPORT.html) | Phase A 측정 결과 — 32 APIs × 2 SFs contention grid (38h), 4 작업 유형 분류, Codex 가설 검증 (43%→81%). |

## Method

전체 파이프라인 (Stage 0-8) 상세는 [PLAN.md](https://github.com/jeff8287/hybrid-bench/blob/master/dev/260507_api_pe_model/PLAN.md) 참조.

## Tooling

리포트 자동 배포: `.claude/skills/publish-report-html/` skill (markdown → HTML → GitHub Pages).
