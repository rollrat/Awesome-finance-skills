---
name: alphaear-news
description: 실시간 금융 뉴스, 통합 트렌드 리포트, 금융 시장 예측 데이터를 가져옵니다. 사용자가 실시간 금융 뉴스, 여러 금융 소스(웨이보, 지후, 화얼가이젠원 등)의 트렌드 리포트, 또는 Polymarket 금융 시장 예측 데이터가 필요할 때 사용합니다.
---

# AlphaEar 뉴스 스킬

## 개요

실시간 인기 뉴스를 가져오고, 통합 트렌드 리포트를 생성하며, Polymarket 예측 데이터를 조회합니다.

## 기능

### 1. 인기 뉴스 및 트렌드 가져오기

`scripts/news_tools.py`의 `NewsNowTools`를 사용합니다.

-   **뉴스 가져오기**: `fetch_hot_news(source_id, count)`
    -   유효한 `source_id` 목록은 [sources.md](references/sources.md)를 참고하세요 (예: `cls`, `weibo`).
-   **통합 리포트**: `get_unified_trends(sources)`
    -   여러 소스의 주요 뉴스를 집계합니다.

### 2. 예측 시장 데이터 가져오기

`scripts/news_tools.py`의 `PolymarketTools`를 사용합니다.

-   **시장 요약**: `get_market_summary(limit)`
    -   활성 예측 시장의 포맷된 리포트를 반환합니다.

## 의존성

-   `requests`, `loguru`
-   `scripts/database_manager.py` (로컬 DB)
