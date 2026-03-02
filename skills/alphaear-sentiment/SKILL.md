---
name: alphaear-sentiment
description: FinBERT 또는 LLM을 사용하여 금융 텍스트의 감성을 분석합니다. 사용자가 금융 텍스트 시장의 감성(긍정/부정/중립)과 점수를 파악해야 할 때 사용합니다.
---

# AlphaEar 감성 분석 스킬

## 개요

금융 텍스트에 특화된 감성 분석 기능을 제공하며, FinBERT(로컬 모델)와 LLM 기반 분석 모드를 모두 지원합니다.

## 기능

### 1. 감성 분석 (FinBERT / 로컬)

`scripts/sentiment_tools.py`를 사용하여 FinBERT 기반 고속 로컬 감성 분석을 수행합니다.

**주요 메서드:**

-   `analyze_sentiment(text)`: 로컬 FinBERT 모델을 사용하여 감성 점수와 레이블을 반환합니다.
    -   **반환값**: `{'score': float, 'label': str, 'reason': str}`.
    -   **점수 범위**: -1.0(부정) ~ 1.0(긍정).
-   `batch_update_news_sentiment(source, limit)`: 데이터베이스의 미분석 뉴스를 일괄 처리합니다 (FinBERT 전용).

### 2. 감성 분석 (LLM / 에이전틱)

더 높은 정확도나 추론 능력이 필요한 경우, **에이전트(당신)**가 아래 프롬프트를 사용하여 LLM을 직접 호출해 분석하고, 필요 시 데이터베이스를 업데이트합니다.

#### 감성 분석 프롬프트

로컬 도구가 부족하거나 추론이 필요한 경우 이 프롬프트를 사용합니다.

```markdown
다음 금융/뉴스 텍스트의 감성 극성을 분석하세요.
엄격한 JSON 형식으로 반환하세요:
{"score": <float: -1.0~1.0>, "label": "<positive/negative/neutral>", "reason": "<간단한 이유>"}

텍스트: {text}
```

**점수 기준:**
- **긍정 (0.1 ~ 1.0)**: 낙관적 뉴스, 실적 성장, 정책 지원 등.
- **부정 (-1.0 ~ -0.1)**: 손실, 제재, 주가 하락, 비관론.
- **중립 (-0.1 ~ 0.1)**: 사실 보도, 횡보 움직임, 영향 불분명.

#### 헬퍼 메서드
- `update_single_news_sentiment(id, score, reason)`: 수동 분석 결과를 데이터베이스에 저장합니다.

## 의존성

-   `torch` (FinBERT용)
-   `transformers` (FinBERT용)
-   `sqlite3` (내장)

`DatabaseManager`가 올바르게 초기화되어 있어야 합니다.
