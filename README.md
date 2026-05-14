# hybrid-bench reports

Public HTML reports for the [hybrid-bench](https://github.com/jeff8287/hybrid-bench) research project — Intel Lunar Lake (4P+4E) 하이브리드 CPU 의 pandas 작업 자동 튜닝.

## Reports

| Date | Report | Description |
|------|--------|-------------|
| 2026-05-15 | [**Phase A Final — Narrative Report**](https://jeff8287.github.io/hybrid-bench-reports/PHASE_A_FINAL_REPORT.html) | 종합 보고서. 7 Discoveries (curve-shape features → 3+1 clusters → SF-aware drift → light-calib protocol → unseen API gen → boundary robustness → honest limits). 32 APIs × 3 SFs (1/2/5) × 24 cells × 13 reps. LOOCV 81% in-distribution. |

## Project structure (high-level)

```
bpd/                                       # 라이브러리
├── auto_ratio.py                          # public predict_ratio() API (SF-aware)
├── models/pe_ratio_model_lunar_lake_sf_aware.json
└── ops/{tpch_ops, extended_ops}.py        # 32 + 5 workloads

dev/260507_api_pe_model/                   # 실험 디렉토리
├── 00-data-prep ~ 09-tier2-unseen/        # 10 stages
└── PHASE_A_FINAL_REPORT.md                # 본 보고서의 소스
```

## Method (high-level)

전체 파이프라인 (Stage 0-9) 상세는 [PLAN.md](https://github.com/jeff8287/hybrid-bench/blob/master/dev/260507_api_pe_model/PLAN.md) 참조.

### Phase A 측정 규모
- 32 APIs × 3 SFs (1, 2, 5) × 24 cells × 13 reps = 9,216 cell measurements
- 총 wall: ~80h (multiple sessions)
- 0 errors, AC-04 PASS

### Phase A 핵심 결과
- LOOCV (in-distribution): **81% pass** (26/32 ≤ 15% MAPE)
- SF-aware cluster drift: 7/21 workloads (filter, groupby_agg, ...) 가 SF=5 에서 linear → hash
- C_linear cluster MAPE: 6.8-7.5% (robust across SFs)
- C0_hash cluster MAPE: 12-23% (heterogeneous, especially SF=5)
- predict_ratio overhead: < 5 μs per call

## Tooling

리포트 자동 배포: `.claude/skills/publish-report-html/` (markdown → HTML → GitHub Pages).
