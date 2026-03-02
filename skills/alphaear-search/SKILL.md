---
name: alphaear-search
description: 금융 웹 검색 및 로컬 컨텍스트 검색을 수행합니다. 사용자가 웹(Jina/DDG/Baidu)에서 일반 금융 정보를 검색하거나 로컬 문서 저장소(RAG)에서 금융 정보를 조회해야 할 때 사용합니다.
---

# AlphaEar 검색 스킬

## 개요

웹 검색(Jina/DDG/Baidu)과 로컬 RAG 검색을 통합한 검색 기능을 제공합니다.

## 기능

### 1. 웹 검색

`scripts/search_tools.py`의 `SearchTools`를 사용합니다.

-   **검색**: `search(query, engine, max_results)`
    -   엔진: `jina`, `ddg`, `baidu`, `local`.
    -   반환값: JSON 문자열(요약) 또는 `search_list`를 통한 `List[Dict]`.
-   **스마트 캐시 (에이전틱)**: 중복 검색을 피하려면 `references/PROMPTS.md`의 **검색 캐시 관련성 프롬프트**를 사용합니다. 캐시를 먼저 읽고 사용 가능 여부를 판단합니다.
-   **집계 검색**: `aggregate_search(query)`
    -   여러 엔진의 결과를 통합합니다.

### 2. 로컬 RAG

`scripts/hybrid_search.py` 또는 `engine='local'`을 설정한 `SearchTools`를 사용합니다.

-   **검색**: 로컬 `daily_news` 데이터베이스를 검색합니다.

## 의존성

-   `duckduckgo-search`, `requests`
-   `scripts/database_manager.py` (검색 캐시 및 로컬 뉴스)
