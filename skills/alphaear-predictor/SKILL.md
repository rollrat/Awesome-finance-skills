---
name: alphaear-predictor
description: Kronos 모델을 사용하는 시장 예측 스킬입니다. 사용자가 금융 시장 시계열 예측 또는 뉴스를 반영한 금융 시장 조정이 필요할 때 사용합니다.
---

# AlphaEar 예측기 스킬

## 개요

Kronos 모델(`KronosPredictorUtility`)을 활용하여 시계열 예측을 수행하고, 뉴스 감성에 기반해 예측값을 조정합니다.

## 기능

### 1. 시장 트렌드 예측

**워크플로우:**
1.  **기본 예측 생성**: `scripts/kronos_predictor.py`의 `KronosPredictorUtility`를 사용하여 기술적/정량적 예측을 생성합니다.
2.  **예측 조정 (에이전틱)**: `references/PROMPTS.md`의 **예측 조정 프롬프트**를 사용하여 최신 뉴스/논리를 바탕으로 수치를 주관적으로 조정합니다.

**주요 도구:**
-   `KronosPredictorUtility.get_base_forecast(df, lookback, pred_len, news_text)`: `List[KLinePoint]`를 반환합니다.

**사용 예시 (Python):**

```python
from scripts.utils.kronos_predictor import KronosPredictorUtility
from scripts.utils.database_manager import DatabaseManager

db = DatabaseManager()
predictor = KronosPredictorUtility()

# 예측 수행
forecast = predictor.predict("600519", horizon="7d")
print(forecast)
```

## 설정

이 스킬은 **Kronos** 모델과 임베딩 모델이 필요합니다.

1.  **Kronos 모델**:
    -   프로젝트 루트에 `exports/models` 디렉토리가 있어야 합니다.
    -   학습된 뉴스 프로젝터 가중치(예: `kronos_news_v1.pt`)를 `exports/models/`에 배치하세요.
    -   또는 기본 모델에 의존합니다(자동 다운로드).

2.  **환경 변수**:
    -   `EMBEDDING_MODEL`: 임베딩 모델의 경로 또는 이름 (기본값: `sentence-transformers/all-MiniLM-L6-v2`).
    -   `KRONOS_MODEL_PATH`: 모델 로딩 경로를 오버라이드할 선택적 경로.

## 의존성

-   `torch`
-   `transformers`
-   `sentence-transformers`
-   `pandas`
-   `numpy`
-   `scikit-learn`
