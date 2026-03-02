---
name: alphaear-logic-visualizer
description: 복잡한 금융 전달 체계나 금융 논리 흐름을 설명하기 위한 금융 논리 다이어그램(예: Draw.io XML)을 생성하고 시각화합니다.
---

# AlphaEar 논리 시각화 스킬

## 개요

논리 흐름의 시각적 표현을 전문으로 생성하며, 특히 Draw.io XML 호환 다이어그램을 출력합니다. 투자 논거나 시그널 전달 체계를 시각화하는 데 유용합니다.

## 기능

### 1. Draw.io 다이어그램 생성 (에이전틱 워크플로우)

**에이전트(당신)**가 시각화 담당자입니다. `references/PROMPTS.md`의 프롬프트를 사용하여 XML을 생성합니다.

**워크플로우:**
1.  **XML 생성**: `references/PROMPTS.md`의 **Draw.io XML 생성 프롬프트**를 사용하여 논리 체계를 XML로 변환합니다.
2.  **저장/렌더링**: `scripts/visualizer.py`의 `render_drawio_to_html(xml_content, filename)` 메서드를 사용하여 XML을 사용자가 볼 수 있는 HTML 파일로 저장합니다.

**사용 예시 (개념적):**
- **에이전트 작업**: "전달 체계에 대한 Draw.io XML을 생성하겠습니다..."
- **도구 호출**: `visualizer.render_drawio_to_html(xml_content="<mxGraphModel>...", filename="chain_visual.html")`

## 의존성

-   없음 (문자열 조작을 위한 표준 라이브러리만 사용).
