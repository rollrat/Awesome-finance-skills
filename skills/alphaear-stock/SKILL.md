---
name: alphaear-stock
description: A주/홍콩/미국 금융 주식 종목 코드를 검색하고 금융 주가 히스토리를 조회합니다. 사용자가 종목 코드, 최근 주가 변동, 또는 특정 기업의 주식 정보를 요청할 때 사용합니다.
---

# AlphaEar 주식 스킬

## 개요

A주/홍콩/미국 주식의 종목 코드를 검색하고 과거 주가 데이터(OHLCV)를 조회합니다.

## 기능

### 1. 종목 검색 및 데이터 조회

`scripts/stock_tools.py`의 `StockTools`를 사용합니다.

-   **종목 검색**: `search_ticker(query)`
    -   종목 코드 또는 기업명으로 퍼지 검색합니다 (예: "마오타이", "600519").
    -   반환값: `{code, name}` 형태의 리스트.
-   **주가 조회**: `get_stock_price(ticker, start_date, end_date)`
    -   OHLCV 데이터가 담긴 DataFrame을 반환합니다.
    -   날짜 형식: "YYYY-MM-DD".

## 의존성

-   `pandas`, `requests`, `akshare`, `yfinance`
-   `scripts/database_manager.py` (주식 테이블)
