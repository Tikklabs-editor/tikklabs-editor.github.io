---
title: "영상 제작 SSD 용량 계산기 — 클립·원본·캐시·백업"
description: "매일 만드는 영상의 실제 파일 크기로 월 저장량과 보관 기간, 작업용 SSD 및 백업 공간을 계산해 보세요."
date: 2026-11-03T16:00:00+09:00
lastmod: 2026-11-03T16:00:00+09:00
type: "page"
draft: false
showDate: false
showReadingTime: false
showWordCount: false
showToc: false
---

AI 영상 생성과 편집에서는 출력물뿐 아니라 참고 원본, 중간 파일과 백업이 쌓여 저장공간이 부족해지곤 해. 이 계산기는 **실제 파일 크기와 작업량**을 기준으로 필요한 용량을 추정해. 별도 가입이나 업로드는 필요 없어.

<div class="tkk-storage" id="tkk-storage">
  <div class="tkk-intro"><span class="tkk-eyebrow">FREE TOOL · LOCAL CALCULATION</span><h2>내 작업량으로 계산하기</h2><p>입력한 정보는 이 페이지에서만 계산하며 서버로 전송하지 않아. 결과는 10진 GB·TB(1TB=1,000GB) 기준이야.</p></div>
  <form id="tkk-form">
    <div class="tkk-inputs">
      <label>하루 생성하는 클립 수 <input id="tkk-clips" type="number" inputmode="numeric" min="1" max="100000" step="1" value="12" required><small>최종 결과물과 시행착오로 보관하는 영상 모두 포함</small></label>
      <label>클립 평균 파일 크기 (MB) <input id="tkk-size" type="number" inputmode="decimal" min="0.01" max="100000" step="any" value="80" required><small>실제 출력 파일 하나의 속성에서 확인하는 게 가장 정확해</small></label>
      <label>한 달 작업일 수 <input id="tkk-days" type="number" inputmode="numeric" min="1" max="31" step="1" value="20" required></label>
      <label>하루 추가 원본 파일 (GB) <input id="tkk-source" type="number" inputmode="decimal" min="0" max="100000" step="any" value="1" required><small>촬영본·참고 이미지·외부에서 받은 소스 등. 모델 파일 설치 용량은 별도</small></label>
      <label>출력물·원본 보관 기간 (개월) <input id="tkk-months" type="number" inputmode="numeric" min="1" max="60" step="1" value="3" required></label>
      <label>작업 캐시 (월간 출력량 대비) <select id="tkk-cache"><option value="0">0배 · 제외</option><option value="0.5" selected>0.5배 · 가벼운 작업</option><option value="1">1배 · 보통</option><option value="2">2배 · 임시 파일이 많은 작업</option><option value="3">3배 · 보수적</option></select><small>캐시는 작업 중 필요한 최대 공간의 가정치이며 장기 보관량에 더하지 않아</small></label>
      <label>별도 백업 사본 수 <select id="tkk-backups"><option value="0">0부 · 계산에서 제외</option><option value="1" selected>1부 · 별도 디스크</option><option value="2">2부 · 서로 다른 위치</option></select><small>백업은 작업용 SSD와 구분하여 계산</small></label>
    </div>
    <button class="tkk-run" type="submit">필요 용량 계산</button>
    <p role="alert" id="tkk-error" hidden></p>
  </form>
  <section class="tkk-results" aria-label="저장공간 계산 결과" aria-live="polite">
    <div class="tkk-primary"><span>여유 공간 20%를 고려한 작업용 용량</span><strong id="tkk-recommend">—</strong><small>일반적인 표시 용량 중 조건을 충족하는 다음 단계. 속도·내구성·용량 단위 변환은 별도 확인</small></div>
    <div class="tkk-metrics">
      <div><span>월간 영상 파일</span><strong id="tkk-monthlyvideo">—</strong></div>
      <div><span>월간 원본 + 영상</span><strong id="tkk-monthlytotal">—</strong></div>
      <div><span>보관 기간 누적</span><strong id="tkk-archive">—</strong></div>
      <div><span>작업 캐시</span><strong id="tkk-temporary">—</strong></div>
      <div><span>작업 드라이브 사용량</span><strong id="tkk-active">—</strong></div>
      <div><span>별도 백업 보관량</span><strong id="tkk-backup">—</strong></div>
    </div>
    <p class="tkk-footnote" id="tkk-equation">—</p>
  </section>
</div>

<style>
.tkk-storage { --tkk-edge:#dcd9d3;--tkk-ink:#2c3334;--tkk-soft:#696f6c;--tkk-paper:#f5f3ee;--tkk-accent:#45655e; color:var(--tkk-ink);margin:2.2rem 0 3.5rem;font-size:1rem }
.tkk-storage * { box-sizing:border-box }
.tkk-storage .tkk-intro{margin-bottom:1.5rem}
.tkk-storage .tkk-eyebrow{display:block;color:var(--tkk-accent);font-size:.72rem;font-weight:650;letter-spacing:.13em}
.tkk-storage h2{font-weight:650;letter-spacing:-.025em;font-size:1.65rem;margin:.4rem 0 .65rem}
.tkk-storage .tkk-intro p,.tkk-storage small,.tkk-storage .tkk-footnote{color:var(--tkk-soft)}
.tkk-storage .tkk-inputs{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:1.15rem 1.5rem}
.tkk-storage label{display:flex;flex-direction:column;font-weight:600;font-size:.92rem;gap:.45rem}
.tkk-storage label small{font-weight:400;font-size:.78rem;line-height:1.55}
.tkk-storage input,.tkk-storage select{font:inherit;width:100%;min-height:2.9rem;background:transparent;border:1px solid var(--tkk-edge);border-radius:6px;color:inherit;padding:.65rem .75rem}
.tkk-storage input:focus-visible,.tkk-storage select:focus-visible,.tkk-storage button:focus-visible{outline:2px solid var(--tkk-accent);outline-offset:3px}
.tkk-storage .tkk-run{margin:1.55rem 0 0;background:var(--tkk-accent);color:#fff;border:0;border-radius:6px;font:inherit;font-weight:600;cursor:pointer;padding:.8rem 1.4rem}
.tkk-storage .tkk-results{margin-top:2.2rem;border-top:1px solid var(--tkk-edge);padding-top:1.5rem}
.tkk-storage .tkk-primary{background:var(--tkk-paper);border:1px solid var(--tkk-edge);border-radius:8px;padding:1.6rem 1.7rem;display:flex;flex-direction:column;gap:.45rem}
.tkk-storage .tkk-primary span{font-weight:600;font-size:.89rem}
.tkk-storage .tkk-primary strong{font-size:clamp(1.8rem,4vw,2.5rem);font-weight:650;letter-spacing:-.04em}
.tkk-storage .tkk-primary small{max-width:38rem}
.tkk-storage .tkk-metrics{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:1rem;padding:1.5rem 0}
.tkk-storage .tkk-metrics div{border-bottom:1px solid var(--tkk-edge);padding-bottom:.8rem;display:flex;flex-direction:column;gap:.2rem}
.tkk-storage .tkk-metrics span{font-size:.78rem;color:var(--tkk-soft)}
.tkk-storage .tkk-metrics strong{font-size:1.2rem;letter-spacing:-.02em}
.tkk-storage .tkk-footnote{font-size:.8rem;line-height:1.7;margin:.3rem 0}
.tkk-storage #tkk-error{font-size:.85rem;color:#a12d2d;margin:.7rem 0}
.dark .tkk-storage {--tkk-edge:#4a4e4c;--tkk-ink:#e6e7e3;--tkk-soft:#adb3ae;--tkk-paper:#313836;--tkk-accent:#9bc1b3}
.dark .tkk-storage .tkk-run{color:#14251e}
.dark .tkk-storage #tkk-error{color:#ffb8b8}
@media(max-width:700px){.tkk-storage .tkk-inputs{grid-template-columns:1fr}.tkk-storage .tkk-metrics{grid-template-columns:repeat(2,minmax(0,1fr))}}
</style>
<script>
(function () {
  "use strict";
  const estimate = function estimate(v) {
  const monthlyVideoGb = v.clipsPerDay * v.mbPerClip * v.daysPerMonth / 1000;
  const monthlySourceGb = v.sourceGbPerDay * v.daysPerMonth;
  const monthlyRetainedGb = monthlyVideoGb + monthlySourceGb;
  const archiveGb = monthlyRetainedGb * v.retentionMonths;
  const workCacheGb = monthlyVideoGb * v.cacheRatio;
  const activeGb = archiveGb + workCacheGb;
  const plannedGb = activeGb / 0.8;
  const backupGb = archiveGb * v.backupCopies;
  const capacitiesTb = [0.5,1,2,4,8,12,16,24,32];
  const recommendedTb = capacitiesTb.find(c => c * 1000 >= plannedGb) ?? null;
  return {monthlyVideoGb,monthlySourceGb,monthlyRetainedGb,archiveGb,workCacheGb,activeGb,plannedGb,backupGb,recommendedTb};
};
  const root = document.getElementById("tkk-storage");
  if (!root) return;
  const byId = (id) => root.querySelector("#" + id);
  const numeric = (id, minimum, maximum) => {
    const el = byId(id);
    const value = Number(el.value);
    if (!el.value.trim() || !Number.isFinite(value) || value < minimum || value > maximum || (el.step === "1" && !Number.isInteger(value))) {
      throw new Error("입력값을 확인해 줘: " + el.closest("label").firstChild.textContent.trim());
    }
    return value;
  };
  const gb = (n) => n >= 1000 ? (n / 1000).toLocaleString("ko-KR",{maximumFractionDigits:2}) + " TB" : n.toLocaleString("ko-KR",{maximumFractionDigits:2}) + " GB";
  function refresh(event) {
    if (event) event.preventDefault();
    const error = byId("tkk-error");
    try {
      const v = {
        clipsPerDay:numeric("tkk-clips",1,100000), mbPerClip:numeric("tkk-size",0.01,100000),
        daysPerMonth:numeric("tkk-days",1,31), sourceGbPerDay:numeric("tkk-source",0,100000),
        retentionMonths:numeric("tkk-months",1,60), cacheRatio:numeric("tkk-cache",0,3),
        backupCopies:numeric("tkk-backups",0,2)
      };
      const r = estimate(v);
      byId("tkk-monthlyvideo").textContent = gb(r.monthlyVideoGb);
      byId("tkk-monthlytotal").textContent = gb(r.monthlyRetainedGb);
      byId("tkk-archive").textContent = gb(r.archiveGb);
      byId("tkk-temporary").textContent = gb(r.workCacheGb);
      byId("tkk-active").textContent = gb(r.activeGb);
      byId("tkk-backup").textContent = gb(r.backupGb);
      byId("tkk-recommend").textContent = r.recommendedTb === null ? "32 TB 초과 · 별도 설계 필요" : r.recommendedTb.toLocaleString("ko-KR") + " TB";
      byId("tkk-equation").textContent = "월간 보관 = (클립 수 × 클립 MB ÷ 1,000 + 하루 원본 GB) × 작업일수. 작업 사용량 = 월간 보관 × 보관 개월수 + 월간 영상량 × 캐시 배수. 권장 최소 용량 = 작업 사용량 ÷ 0.8 (여유 20%). 별도 백업 = 보관 파일 총량 × 사본 수. 제조사 표기 TB와 실제 OS 표시 용량은 다를 수 있어.";
      error.hidden=true;
    } catch (e) {
      error.textContent=e.message;error.hidden=false;
    }
  }
  byId("tkk-form").addEventListener("submit",refresh);
  refresh();
})();
</script>

## 계산 결과를 해석하는 방법

- **작업용 드라이브:** 보관 파일과 현재 작업 중의 임시 캐시가 함께 들어갈 공간이야. 약 20%를 비워 놓는다는 조건으로 계산했어.
- **별도 백업:** 같은 SSD의 다른 폴더에 복사하는 것은 물리적 고장에 대비한 별도 백업이 아니야. 실제로 별도 디스크 또는 독립된 보관 위치가 있어야 해.
- **주의할 점:** 여기서는 모델 체크포인트, 운영체제·앱 설치, 영상 중복 다운로드, 압축 해제 후 파일 크기, 클라우드 요금 등을 자동으로 추정하지 않아. 큰 모델 파일을 계속 받는다면 별도 용량을 직접 더해야 해.

계산은 방문자가 입력한 수치에 대한 산술 추정일 뿐, 특정 제품의 실제 성능이나 수명을 보증하지 않아. 특히 출력 동영상의 크기는 해상도만이 아니라 길이·코덱·비트레이트에 따라 달라지므로 **이미 만든 결과물의 평균 크기**를 입력하는 편이 좋아.

### 근거와 참고

Adobe의 [Premiere 저장소 권장 사항](https://helpx.adobe.com/kr/premiere/desktop/get-started/technical-requirements/storage-recommendations.html)은 OS/앱, 미디어, 캐시의 역할을 구분해 설명해. [Puget Systems의 영상 편집 저장소 가이드](https://www.pugetsystems.com/labs/articles/understanding-storage-for-video-editing-2286/)도 미디어·캐시 분리와 대역폭을 다뤄. 이 계산기의 **20% 여유와 캐시 배수는 제조사 공인 수치가 아니라 사용자가 조절하는 계획 가정**이야.

이 페이지는 2026년 11월 3일에 산술 검증을 거쳐 공개한 첫 실험용 도구야. 광고·제휴 링크를 아직 포함하지 않으며, 특정 SSD를 써 봤다고 주장하지 않아.
