---
title: "ComfyUI 설치와 첫 이미지 생성: Windows·SDXL 시작 가이드"
date: 2026-03-31T16:00:00+09:00
lastmod: 2026-10-05T14:20:00+09:00
draft: false
authors: ["tikklabs-editor"]
categories: ["Local AI"]
tags: ["ComfyUI", "SDXL", "Local AI"]
slug: "it-productivity-local-ai-guide"
translationKey: "local-ai-guide"
featureimage: "img/editorial/local-ai.webp"
description: "Windows에서 ComfyUI를 준비하고 SDXL로 첫 이미지를 만드는 절차, 기본 오류 확인법과 모델 라이선스 주의점을 안내합니다."
showToc: true
---

이 글은 [로컬 AI 입문 필러 가이드](/ko/local-ai/)의 다음 단계입니다. 로컬 AI와 오픈소스 AI의 차이, 가능한 제작 영역, 비용 구조를 먼저 알고 싶다면 필러 가이드부터 읽으세요.

여기서는 범위를 **Windows에서 ComfyUI를 준비하고 SDXL로 첫 이미지 한 장을 확인하는 과정**으로 좁힙니다. 설치만 해둔 독자는 설치를 반복하지 말고, 현재 실행 방식과 모델 폴더를 확인한 뒤 이미지 생성 단계부터 진행하세요. 특정 PC의 생성 속도를 측정한 벤치마크는 아닙니다.

## 로컬 AI가 맞는 작업부터 고르세요

| 작업 상황 | 먼저 검토할 방식 |
|---|---|
| 썸네일 배경·삽화처럼 반복 생성이 많고 PC를 보유한 경우 | 로컬 이미지 생성으로 일부 작업 이전 |
| 월 사용량이 적고 설정에 시간을 쓰기 어려운 경우 | 무료 제공량 또는 필요한 달만 구독 |
| 이미지·음성·영상이 모두 필요하고 마감이 촉박한 경우 | 로컬과 유료 서비스 병행 |
| 고객 자료를 다루는 경우 | 사용 모델뿐 아니라 외부 API 연결·업로드 설정도 확인 |

**로컬 이미지 생성, 로컬 TTS, 로컬 챗봇은 같은 작업이 아닙니다.** 이미지 도구를 설치했다고 음성 합성까지 자동으로 준비되는 것은 아닙니다.

![내 PC에서 처리하는 구성과 외부 API를 쓰는 구성의 차이](img/editorial/local-scope-ko.svg "자체 작성한 구성도입니다. 로컬 도구에서도 외부 API를 선택하면 데이터가 외부로 전달됩니다.")

## Windows에서 ComfyUI 시작하기

1. [ComfyUI 공식 Windows 설치 안내](https://docs.comfy.org/installation/desktop/windows)에서 설치 파일을 받습니다. 검색 광고나 이름이 비슷한 사이트를 경유할 필요는 없습니다.
2. 설치 프로그램을 실행하고 Comfy Desktop을 엽니다. 첫 화면에서 ComfyUI 설치 인스턴스를 만듭니다. 모델과 결과물을 둘 저장 공간을 확인합니다.
3. [공식 SDXL Base 모델 페이지](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)에서 모델 파일과 라이선스를 확인합니다. 이 예시는 `sd_xl_base_1.0.safetensors`를 사용합니다.
4. 해당 ComfyUI 인스턴스의 `models/checkpoints` 폴더에 모델을 넣습니다. Desktop 버전과 사용자가 정한 설치 위치에 따라 전체 경로는 달라집니다.
5. [공식 텍스트→이미지 예제](https://docs.comfy.org/tutorials/basic/text-to-image)의 기본 흐름을 불러온 뒤, **Load Checkpoint**에서 SDXL Base를 선택합니다. 예제에 표시된 SD1.5 모델을 그대로 선택하는 것과 구분해야 합니다.
6. SDXL 예제 기준으로 **Empty Latent Image**를 1024×1024, 한 번에 생성할 장수를 1로 설정합니다. 처음에는 추가 LoRA나 커스텀 노드 없이 시작합니다.
7. 긍정 프롬프트에 `a ceramic mug on a wooden desk, soft daylight, simple background`처럼 원하는 장면을 입력하고 **Queue** 또는 `Ctrl+Enter`로 실행합니다.
8. **Save Image**에 결과가 표시되는지 확인합니다. 같은 장면을 몇 번 만들어 품질·소요 시간·수정 횟수를 기록합니다.

[SDXL 공식 예제](https://comfyanonymous.github.io/ComfyUI_examples/sdxl/)는 Base 체크포인트를 일반 체크포인트처럼 사용할 수 있다고 안내합니다. Refiner는 첫 실행에 필수로 추가할 필요가 없습니다.

### 첫 실행이 안 될 때

| 증상 | 먼저 확인할 항목 |
|---|---|
| 모델 선택에 파일이 안 보임 | 현재 실행한 인스턴스의 checkpoints 폴더에 넣었는지 확인하고 새로고침·재시작 |
| 메모리 부족 오류 | 동시 생성 장수를 1로 줄이고 GPU를 사용하는 다른 앱 종료. 필요하면 더 가벼운 모델 검토 |
| 누락된 노드 메시지 | 추가 플러그인을 요구하는 워크플로인지 확인하고 기본 예제로 돌아가기 |
| 생성은 되지만 결과가 마음에 안 듦 | 모델·프롬프트·해상도를 하나씩 바꾸고 비교 |

ComfyUI 실행 가능 여부와 특정 모델의 성능은 별개입니다. 필요한 메모리는 모델·해상도·동시 작업에 따라 달라집니다. 먼저 보유 PC로 시험하고, 결과와 작업 시간을 확인한 뒤 장비 구매를 판단하세요.

## 무료 모델과 상업용 사용 허가는 다릅니다

SDXL Base 1.0은 **CreativeML Open RAIL++-M** 라이선스로 제공됩니다. 사용 제한이 있는 라이선스이며, 파생 모델이나 LoRA의 추가 조건은 별도로 확인해야 합니다. 모델 이름이 ‘Stable Diffusion 계열’이라는 것만으로 모두 같은 조건이 적용되는 것은 아닙니다.

TTS에서도 이 구분이 중요합니다. **XTTS-v2의 공개 라이선스는 모델과 출력물의 비상업적 사용만 허용합니다.** 유료 납품이나 수익 콘텐츠에 쓸 수 있는 무료 음성 모델로 일괄 추천할 수 없습니다. 음성 모델을 고를 때는 지원 언어·음성 품질과 함께 실제 라이선스를 확인하세요.

- [SDXL Base 라이선스 원문](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/LICENSE.md)
- [XTTS-v2 라이선스 원문](https://huggingface.co/coqui/XTTS-v2/blob/main/LICENSE.txt)

## 구독을 끊기 전, 완성된 결과물 기준으로 비교하세요

간단한 월 비용 계산은 다음과 같습니다.

**로컬 월 비용 = 추가 전기료 + 장비 비용의 월 배분액 + 실제로 발생하는 유지 비용**

이미 가진 PC를 쓰는 경우와 AI 때문에 새 장비를 사는 경우는 계산이 다릅니다. 여기에 원하는 결과를 얻을 때까지 쓰는 시간도 함께 기록하세요. 단순 생성 장수보다 **실제로 사용할 수 있는 이미지 한 장을 완성하는 비용**이 중요합니다.

처음부터 모든 구독을 끊기보다 반복되는 한 작업만 로컬로 옮겨 보세요. 품질과 작업 시간이 만족스러우면 그 부분의 구독 비용을 줄이고, 대체가 어려운 작업에는 유료 서비스를 남기는 방식이 현실적입니다.

확인 기준: 2026년 10월 5일 ComfyUI 공식 문서와 모델 배포자의 라이선스.

[함께 읽기: 디지털 과부하와 작업 전환 줄이기](/ko/post/stone-age-brain-vs-gpt/)

[로컬 AI 시리즈 전체 목차](/ko/local-ai/)
