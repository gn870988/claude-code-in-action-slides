---
theme: default
title: AI輔助開發流程實戰
favicon: /claude-icon.svg
transition: slide-left
fonts:
  sans: Noto Sans TC
drawings:
  persist: false
layout: cover
class: cover-slide
---

<!-- 第 1 頁：封面頁 (Cover)
     layout 與 background 寫在 headmatter，直接作用於第一頁 -->

<div class="cover-overlay">
  <div class="cover-title-block">
    <div class="cover-main-title">AI 輔助開發流程實<span class="title-easter">戰<img src="/clawd_1.gif" class="easter-gif" /></span></div>
    <div class="cover-sub-title">Ticket → PR 全流程 + 大改版策略</div>
    <div class="cover-divider" />
  </div>

  <div class="cover-meta">
    <span class="cover-author">Vincent Yu</span>
    <span class="cover-dept">ACL_COE_MyA&amp;PRM · 2026</span>
  </div>
</div>


---
layout: default
class: agenda-slide
---

<!-- 第 2 頁：大綱頁 (Agenda) -->

<div class="agenda-header">
  <div class="agenda-bar" />
  <h1 class="agenda-heading">Agenda</h1>
</div>

<div class="agenda-grid">
  <div class="agenda-item">
    <span class="agenda-num">01</span>
    <span class="agenda-text">
      <span class="agenda-title">現況痛點</span>
      <span class="agenda-sub">我們現在怎麼用 AI，卡在哪裡</span>
    </span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">02</span>
    <span class="agenda-text">
      <span class="agenda-title">方法框架</span>
      <span class="agenda-sub">Agentic 開發、Skills、Agent 分工</span>
    </span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">03</span>
    <span class="agenda-text">
      <span class="agenda-title">實戰 Demo</span>
      <span class="agenda-sub">Ticket 到 PR，小改動與大改版</span>
    </span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">04</span>
    <span class="agenda-text">
      <span class="agenda-title">團隊落地</span>
      <span class="agenda-sub">踩雷案例、守則與防線</span>
    </span>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 3 頁：今天你會帶走什麼 -->

<div class="hook-eyebrow">開場</div>
<h1 class="hook-title">今天你會帶走什麼</h1>

<div class="statement-body">
  <div class="statement-item">
    <span class="statement-num">01</span>
    <span class="statement-text">看完一張 Ticket → PR 的完整節奏<br><span class="statement-sub">用 #6894 實際走過一次，看清楚 AI 在哪裡接手、哪裡該你確認</span></span>
  </div>
  <div class="statement-item">
    <span class="statement-num">02</span>
    <span class="statement-text">大型改版怎麼分段，不靠「塞一句 prompt」做大事<br><span class="statement-sub">Context Pack + 分段 Plan，讓跨多檔的改版可以一段一段走穩</span></span>
  </div>
  <div class="statement-item">
    <span class="statement-num">03</span>
    <span class="statement-text">一份可以推回團隊的 SOP 與防線<br><span class="statement-sub">3 個真實踩雷案例 + 5 條守則，讓 AI 跟著流程走，而不是靠人每次提醒</span></span>
  </div>
</div>

<!--
說話點：
- 這場分享我不教安裝、不講原理，聚焦「我每天怎麼用」
- 三個帶走點對應後面三大段：Demo A / Demo B / SOP
-->

---
layout: default
class: content-slide hook-slide
---

<!-- 第 4 頁：Hook — 你現在怎麼用 AI？ -->

<div class="hook-eyebrow">現況痛點</div>
<h1 class="hook-title">你現在怎麼用 AI？</h1>

<div class="flow-wrap">
  <div class="flow-track">
    <div class="flow-node">
      <div class="flow-node-icon">📋</div>
      <div class="flow-node-name">Azure<br>Ticket</div>
    </div>
    <div class="flow-gap">
      <div class="flow-gap-label">你 copy</div>
      <div class="flow-gap-line"></div>
    </div>
    <div class="flow-node">
      <div class="flow-node-icon">💬</div>
      <div class="flow-node-name">Chat<br>GPT</div>
    </div>
    <div class="flow-gap">
      <div class="flow-gap-label">你 copy</div>
      <div class="flow-gap-line"></div>
    </div>
    <div class="flow-node">
      <div class="flow-node-icon">⌨️</div>
      <div class="flow-node-name">VS<br>Code</div>
    </div>
    <div class="flow-gap">
      <div class="flow-gap-label">你 push</div>
      <div class="flow-gap-line"></div>
    </div>
    <div class="flow-node">
      <div class="flow-node-icon">🔀</div>
      <div class="flow-node-name">GitHub<br>PR</div>
    </div>
  </div>
  <div class="flow-callout">你是 AI 和 codebase 之間的「搬運工」</div>
  <div style="margin-top:0.6rem;text-align:center;font-size:0.95rem;color:var(--m-muted);letter-spacing:0.02em;">
    以 <strong style="color:var(--m-text);">#6894</strong> 這類小改動為例　<strong style="color:var(--m-warm);">15+</strong> Copy-Paste　·　<strong style="color:var(--m-warm);">20+</strong> 切視窗　·　<strong style="color:var(--m-warm);">~1h</strong> 純搬運工時
  </div>
</div>

<div class="hook-pills">
  <div class="hook-pill">AI 沒有你的 codebase context</div>
  <div class="hook-pill">不知道你的 Ticket 要求</div>
  <div class="hook-pill accent">今天要改變這件事 →</div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 4 頁：AI 代理式開發是什麼？ (Chapter 02) -->

<div class="hook-eyebrow">方法框架 · Agentic 開發</div>
<h1 class="hook-title">AI 代理式開發是什麼？</h1>

<div class="compare-wrap">
  <div class="compare-col compare-old">
    <div class="compare-label">傳統用法</div>
    <ul>
      <li>你問一句，AI 答一句</li>
      <li>手動讀、手動貼、手動決定</li>
      <li>每個步驟都要人工介入</li>
    </ul>
  </div>
  <div class="compare-divider">→</div>
  <div class="compare-col compare-new">
    <div class="compare-label">Agentic 用法</div>
    <ul>
      <li>AI 自主執行多個步驟</li>
      <li>讀 Ticket、分析 code、規劃、實作、自查</li>
      <li>人只在節點確認</li>
    </ul>
  </div>
</div>

<div class="compare-keynote" v-click>「你指定目標，AI 走完流程」</div>

<!--
說話點：
- 傳統用法：你問一句，AI 答一句 → 你手動讀、手動貼、手動決定
- Agentic 用法：AI 自主執行多個步驟——讀 Ticket、分析 code、規劃修改、實作、自我 review
- 人只在節點確認
-->

---
layout: default
class: content-slide hook-slide
---

<!-- 第 5 頁：Skills 介紹 (Chapter 03) -->

<div class="hook-eyebrow">方法框架 · Skills</div>
<h1 class="hook-title">Skill = 團隊 SOP 的 AI 版本</h1>

<div class="skills-wrap">
  <div class="skills-gif-block">
    <img src="/matrix-skill.gif" class="skills-gif" />
    <div class="skills-gif-caption">駭客任務：Trinity 瞬間習得直升機駕駛技能</div>
  </div>
  <div class="skills-desc">
    <div class="skills-desc-item">把重複流程寫成 AI 可以照著跑、也能被人驗收的規格</div>
    <div class="skill-flow-card">
      <div class="skill-flow-header">
        <span class="skill-sample-label">Example</span>
        <span class="skill-sample-name">ado-ticket-analysis</span>
      </div>
      <div class="skill-flow-trigger">貼上 ADO Ticket URL</div>
      <div class="skill-flow-steps">
        <div class="skill-flow-step"><span>1</span>解析 Work Item ID</div>
        <div class="skill-flow-step"><span>2</span>讀取 JSON、描述與圖片</div>
        <div class="skill-flow-step"><span>3</span>分析需求、UI 影響與驗收條件</div>
        <div class="skill-flow-step"><span>4</span>產出影響檔案、實作步驟與風險</div>
      </div>
    </div>
    <div class="skill-demo-note">這個 Skill 停在 Analyze / Auto-Plan；等你確認後，才交給後續 Coding 流程</div>
    <div class="skills-others">
      <div class="skills-others-label">這只是其中一個　常用 Skills 還有</div>
      <div class="skills-others-pills">
        <span class="skills-pill"><strong>commit</strong> · 產 commit message</span>
        <span class="skills-pill"><strong>prp-pr</strong> · 開 PR + 寫描述</span>
        <span class="skills-pill"><strong>code-review</strong> · review 留言</span>
        <span class="skills-pill"><strong>plan</strong> · 多階段計畫</span>
        <span class="skills-pill"><strong>tdd</strong> · 測試先行</span>
      </div>
    </div>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 6 頁：AI Agent 比較 (Chapter 03) -->

<div class="hook-eyebrow">方法框架 · Agent 分工</div>
<h1 class="hook-title">Agent 不是排名，是分工</h1>

<div class="agents-wrap">
  <div class="agent-card">
    <img src="/icon-codex.svg" class="agent-icon" />
    <div class="agent-name">Codex</div>
    <div class="agent-role">細心的資深開發者</div>
    <div class="agent-desc">適合 review、查問題、動高風險程式；步調慢一點，但比較不會亂來。</div>
  </div>
  <div class="agent-card agent-main">
    <img src="/claude-icon.svg" class="agent-icon" />
    <div class="agent-name">Claude</div>
    <div class="agent-role">聰明的老鳥</div>
    <div class="agent-desc">適合拆需求、規劃、快速實作；效率很高，但要把驗收標準講清楚。</div>
  </div>
  <div class="agent-card agent-muted">
    <img src="/icon-gemini.svg" class="agent-icon" />
    <div class="agent-name">Gemini</div>
    <div class="agent-role">很會整理，但有想法</div>
    <div class="agent-desc">適合摘要、轉格式、處理大量內容；需求邊界要寫死，不然它會幫你加戲。</div>
  </div>
</div>

<div style="margin-top:1.2rem;font-size:0.82rem;color:var(--m-muted);text-align:center;line-height:1.6;">
  ※ 以上為個人使用體感，非 benchmark 評比　·　目前主力 <strong style="color:var(--m-text);">Claude</strong>　·　Codex 用在 review 與高風險變更　·　Gemini 處理大量文件與摘要
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 7 頁：開發流程全貌 (Chapter 04) -->

<div class="hook-eyebrow">方法框架 · 開發流程全貌</div>
<h1 class="hook-title">開發流程全貌</h1>

<div class="pipeline-wrap">
  <div class="pipeline-track">
    <div class="pipeline-node node-start">
      <div class="pipeline-icon">📋</div>
      <div class="pipeline-name">Ticket</div>
      <div class="pipeline-desc">Skill 自動讀取<br>Azure 需求</div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node">
      <div class="pipeline-icon">🔍</div>
      <div class="pipeline-name">Analyze</div>
      <div class="pipeline-desc">AI 讀 codebase<br>理解影響範圍</div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node">
      <div class="pipeline-icon">📝</div>
      <div class="pipeline-name">Plan</div>
      <div class="pipeline-desc">AI 提案，你確認<br><span class="node-model"><span>Opus 4.7</span><span>GPT-5.5</span></span></div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node">
      <img src="/claude-icon.svg" class="pipeline-icon-img" />
      <div class="pipeline-name">Coding</div>
      <div class="pipeline-desc">AI 實作，你監督<br><span class="node-model"><span>Sonnet 4.6</span><span>GPT-5.4</span></span></div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node">
      <div class="pipeline-icon">✅</div>
      <div class="pipeline-name">Check</div>
      <div class="pipeline-desc">自查 + 測試<br>你確認結果</div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node">
      <div class="pipeline-icon">🚀</div>
      <div class="pipeline-name">PR</div>
      <div class="pipeline-desc">AI 產 Summary<br>你送出</div>
    </div>
    <div class="pipeline-arrow">→</div>
    <div class="pipeline-node node-end">
      <div class="pipeline-icon">👁️</div>
      <div class="pipeline-name">PR Review</div>
      <div class="pipeline-desc">交叉 review<br>人工驗收</div>
    </div>
  </div>

  <div class="demo-pills" v-click>
    <div class="demo-pill demo-pill-a">
      <span class="demo-pill-label">Demo A</span>
      <span class="demo-pill-desc">Ticket → Analyze → Plan → Coding → Check → PR → PR Review　完整走一次</span>
    </div>
    <div class="demo-pill demo-pill-b">
      <span class="demo-pill-label">Demo B</span>
      <span class="demo-pill-desc">重點聚焦　Analyze → Plan → Coding　大型改版如何分段</span>
    </div>
  </div>

  <div class="model-tip" v-click>
    <span class="model-tip-label">模型建議</span>
    <span class="model-tip-item"><span class="model-tip-phase">Plan</span>Opus 4.7 · GPT-5.5</span>
    <span class="model-tip-sep">→</span>
    <span class="model-tip-item"><span class="model-tip-phase">Coding</span>Sonnet 4.6 · GPT-5.4</span>
  </div>
</div>

<!--
說話點：
- Demo A 會走完整個流程
- Demo B 聚焦在大型改版的 Analyze → Plan → Coding 如何分段處理
-->

---
layout: default
class: content-slide hook-slide
---

<!-- 第 8 頁：Demo A 情境說明 (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A</div>
<h1 class="hook-title">Demo A：日常小改動流程</h1>

<div class="demo-a-wrap">
  <div class="demo-ticket-badge">
    <span class="demo-ticket-id">#6894</span>
    <span class="demo-ticket-title">IMR Ship-To 非歐洲國家的 warning</span>
  </div>

  <div class="demo-a-body">
    <div class="demo-a-scenario">
      <div class="demo-a-scenario-label">需求情境</div>
      <div class="demo-a-scenario-desc">
        當 IMR 的 <strong>Ship-To Country</strong> 為<span class="demo-highlight">非歐洲國家</span>時<br>
        在 <strong>Incoterm Location</strong> 欄位下方加上提醒文字
      </div>
      <div class="demo-a-quote">
        "Additional costs will be charged for FOC orders to outside Europe."
      </div>
    </div>
    <div class="demo-a-screenshot">
      <img src="/wi6894.jpeg" class="demo-a-img" />
      <div class="demo-a-img-caption">Shipping Information 表單 ── ① icon 方案 / ② 文字下方方案</div>
    </div>
  </div>

  <div class="demo-a-hint">
    <span class="demo-a-hint-label">注意</span>
    <span>接下來會分三段影片，看 AI 怎麼從 #6894 走到 PR</span>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 9 頁：Demo A Part 1 — Plan & Coding (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A · Part 1</div>
<h1 class="hook-title">Plan → Coding → Commit</h1>

<div class="demo-video-wrap">
  <div class="demo-watch-note">
    <span class="demo-watch-label">觀看重點</span>
    <span>看 AI 如何從 Ticket 推出 Plan，再把確認過的方案落到 code 與 commit</span>
  </div>
  <SmartVideo src="/demo-a-1-plan-coding-commit.mp4" youtube="https://youtu.be/QPVcf1BtdDM" />
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 10 頁：Demo A Part 2 — PR (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A · Part 2</div>
<h1 class="hook-title">Skill 發 PR</h1>

<div class="demo-video-wrap">
  <div class="demo-watch-note">
    <span class="demo-watch-label">觀看重點</span>
    <span>看 Skill 如何產出 PR 描述；送出前仍要由人確認需求、風險與測試結果</span>
  </div>
  <SmartVideo src="/demo-a-2-pr.mp4" youtube="https://youtu.be/SSytN-0pZ8c" />
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 11 頁：Demo A Part 3 — Code Review (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A · Part 3</div>
<h1 class="hook-title">Skill Code Review & 留言</h1>

<div class="demo-video-wrap">
  <div class="demo-watch-note">
    <span class="demo-watch-label">觀看重點</span>
    <span>看另一個 Agent 如何協助 review，把它當成多一道檢查，不取代人工驗收</span>
  </div>
  <SmartVideo src="/demo-a-3-review.mp4" youtube="https://youtu.be/dnvbi9-CNVs" />
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 12 頁：Demo A 重點回顧 (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A</div>
<h1 class="hook-title">剛才發生了什麼？</h1>

<div class="statement-body">
  <div class="statement-item">
    <span class="statement-num">01</span>
    <span class="statement-text">Ticket 直接交給 AI，你只負責確認<br><span class="statement-sub">Skill 自動讀取 ADO 需求、分析影響範圍、提出 Plan——你從「搬運工」變成「審核者」</span></span>
  </div>
  <div v-click class="statement-item">
    <span class="statement-num">02</span>
    <span class="statement-text">Coding 全程有人監督，Commit 自動產生<br><span class="statement-sub">AI 按 Plan 實作，commit message 也由 AI 寫——你的角色是確認方向，不是打字</span></span>
  </div>
  <div v-click class="statement-item">
    <span class="statement-num">03</span>
    <span class="statement-text">PR 與 Review 都有 AI 協助，但最後仍由人驗收<br><span class="statement-sub">Skill 可以產 PR 描述、另一個 Agent 可以協助 Code Review；交叉 review 是多一道防線，不取代測試與人工判斷</span></span>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 13 頁：ROI 對照 (Chapter 05) -->

<div class="hook-eyebrow">實戰 Demo · Demo A</div>
<h1 class="hook-title">省的不是時間，是腦力</h1>

<div class="compare-wrap">
  <div class="compare-col compare-old">
    <div class="compare-label">傳統做法　人類全程動手</div>
    <ul>
      <li>讀 ticket + 切視窗找 code　<strong>~8 min</strong></li>
      <li>寫 code + commit　<strong>~15 min</strong></li>
      <li>開 PR + 寫描述　<strong>~7 min</strong></li>
      <li>自己 code review　<strong>~5 min</strong></li>
    </ul>
    <div style="margin-top:1rem;font-size:1.4rem;font-weight:700;color:var(--m-warm);text-align:center;">人類投入　~35 min　全程在線</div>
  </div>
  <div class="compare-divider">→</div>
  <div class="compare-col compare-new">
    <div class="compare-label">AI 流程　人只在節點確認</div>
    <ul>
      <li>審 Plan + 來回修正　<strong>3–8 min</strong></li>
      <li>看 diff + 抽查邏輯　<strong>2–5 min</strong></li>
      <li>確認 PR Summary 送出　<strong>1–2 min</strong></li>
      <li>看 Review 結論　<strong>1–2 min</strong></li>
    </ul>
    <div style="margin-top:1rem;font-size:1.4rem;font-weight:700;color:var(--m-teal);text-align:center;">4 個 checkpoint　約 7–17 min</div>
  </div>
</div>

<div class="compare-keynote" v-click>從「連續半小時都得在線」變成「4 個 2–5 min 的 checkpoint」<br><span style="font-size:0.95rem;font-weight:500;color:var(--m-muted);">注意力被釋放——AI 跑的時候你可以開另一張 ticket、深入 review 同事 PR、補測試</span></div>

<div style="margin-top:1.2rem;font-size:0.85rem;color:var(--m-muted);text-align:center;">※ 以 #6894 為對照基準；數字為實測區間，會因 ticket 複雜度與熟練度調整</div>

<!--
說話點：
- 重點不是「快了多少」，是「型態改變」——從連續在線變成碎片化 checkpoint
- 傳統 ~35 min 全部都是你連續動腦
- AI 流程 7–17 min 中，分成 4 個 2–5 min 的檢查點
- AI 在跑的時候，你可以開另一張 ticket、深入 review 同事的 PR、補測試
- 真正意義：你的注意力被釋放出來了，不是省時間
- 不講百分比是因為每張 ticket 不同，講「型態」比講「比例」更穩
-->

---
layout: default
class: content-slide hook-slide
---

<!-- 第 14 頁：Demo B 章節開場 / 橋接頁 (Chapter 06) -->

<div class="hook-eyebrow">實戰 Demo · Demo B</div>
<h1 class="hook-title">Demo B：大型改版怎麼做？</h1>

<div class="compare-wrap">
  <div class="compare-col compare-old">
    <div class="compare-label">Demo A　小需求</div>
    <ul>
      <li>單一 Ticket，影響範圍小</li>
      <li>AI 一次掌握範圍，直接走完流程</li>
      <li>Ticket → Plan → Coding → PR</li>
    </ul>
  </div>
  <div class="compare-divider">→</div>
  <div class="compare-col compare-new">
    <div class="compare-label">Demo B　大改版</div>
    <ul>
      <li>跨多個檔案，影響範圍廣</li>
      <li>一次塞太多，脈絡容易不足</li>
      <li>需要拆段 + 固化脈絡</li>
    </ul>
  </div>
</div>

<div class="compare-keynote" v-click>「大任務直接塞，計畫就會失準——需要新策略」</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 15 頁：Context Pack 說明 (Chapter 06) -->

<div class="hook-eyebrow">實戰 Demo · Demo B</div>
<h1 class="hook-title">Context Pack</h1>

<div class="demo-b-wrap">

  <div class="demo-a-quote">
    AI 每次開新對話都需要重新取得 codebase 脈絡——大任務直接丟，context 不足，計畫就會失準。
  </div>

  <div class="ctx-fail-block">
    <div class="ctx-fail-row">
      <span class="ctx-fail-tag">❌ 直接塞</span>
      <span class="ctx-fail-prompt">「幫我重構訂單模組成 DDD」</span>
    </div>
    <div class="ctx-fail-result">→ AI 回 8 個 phase、47 個檔案、無優先順序 &nbsp;<strong>你看完不敢點 Yes</strong></div>
  </div>

  <div class="demo-a-scenario-label">解法：事先讓 AI 分析並整理成 Context Pack，每段對話都帶著進來</div>

  <div class="demo-b-tree">
    <div class="demo-b-tree-root">context/</div>
    <div class="demo-b-tree-items">
      <div class="demo-b-tree-item">
        <span class="demo-b-tree-file">00-project-overview.md</span>
        <span class="demo-b-tree-desc">整體架構、模組關係、現有流程</span>
      </div>
      <div class="demo-b-tree-item">
        <span class="demo-b-tree-file">01-affected-files.md</span>
        <span class="demo-b-tree-desc">受影響範圍與各檔案改動方向</span>
      </div>
      <div class="demo-b-tree-item">
        <span class="demo-b-tree-file">02-design-decision.md</span>
        <span class="demo-b-tree-desc">業務規則與建議實作設計</span>
      </div>
    </div>
  </div>

  <div class="demo-b-approach">
    <span class="demo-b-approach-label">流程</span>
    <span class="demo-b-phase">AI 分析產出 Context Pack</span>
    <span class="demo-b-phase-arrow">→</span>
    <span class="demo-b-phase">帶脈絡提 Phase 計畫</span>
    <span class="demo-b-phase-arrow">→</span>
    <span class="demo-b-phase">Phase 1 執行確認</span>
    <span class="demo-b-phase-arrow">→</span>
    <span class="demo-b-phase">繼續下一段</span>
  </div>

</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 16 頁：Demo B 影片 (Chapter 06) -->

<div class="hook-eyebrow">實戰 Demo · Demo B · Demo</div>
<h1 class="hook-title">Context Pack → 分段實作</h1>

<div class="demo-video-wrap">
  <div class="demo-watch-note">
    <span class="demo-watch-label">觀看重點</span>
    <span>看 Context Pack 如何固定共享脈絡，讓大型改版可以分段計畫、分段確認</span>
  </div>
  <SmartVideo src="/demo-b-context-pack.mp4" youtube="https://youtu.be/Nxtk7qcqJ1w" />
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 17 頁：Demo B 重點回顧 (Chapter 06) -->

<div class="hook-eyebrow">實戰 Demo · Demo B</div>
<h1 class="hook-title">大改版的關鍵：分段與確認</h1>

<div class="statement-body">
  <div class="statement-item">
    <span class="statement-num">01</span>
    <span class="statement-text">AI 不會自動保留完整開發脈絡，大任務直接塞會失控<br><span class="statement-sub">每次開新對話都需要重新提供 codebase、需求與設計判斷；context 不足，計畫就容易失準</span></span>
  </div>
  <div v-click class="statement-item">
    <span class="statement-num">02</span>
    <span class="statement-text">Context Pack：把關鍵脈絡變成可追溯文件<br><span class="statement-sub">先讓 AI 分析 codebase、整理架構與設計判斷；之後每段對話帶著文件進來，讓 AI 有一致的共享上下文</span></span>
  </div>
  <div v-click class="statement-item">
    <span class="statement-num">03</span>
    <span class="statement-text">人只在節點確認，每段做完才進下一段<br><span class="statement-sub">AI 提出 Phase 計畫，你確認順序；Phase 1 做完確認結果，才進 Phase 2——大任務就是這樣一段一段走穩的</span></span>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 18 頁：踩雷前言 (Chapter 07) -->

<div class="hook-eyebrow">團隊落地</div>
<h1 class="hook-title">用了 AI，還是出事了</h1>

<div class="preface-wrap">
  <div class="preface-quote">
    「AI 不會主動告訴你它做錯了——你不問，它不說。」
  </div>
  <div class="preface-body">
    <div class="preface-item">以下三個案例是真實發生過的，不是理論上的風險</div>
    <div class="preface-item">每個案例會直接給出對應的守則</div>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 19 頁：Bad Case 1 -->

<div class="hook-eyebrow">團隊落地 · Bad Case 1</div>
<h1 class="hook-title bc-title">AI 不是不能執行指令，是不能無限制執行指令</h1>

<div class="bc-wrap bc-sop">
  <div class="bc-trigger">
    <span class="bc-section-label">觸發情境</span>
    <span>讓 AI 在 repo 內自由執行 shell 與 file operation</span>
  </div>
  <div class="bc-grid">
    <div class="bc-cell">
      <div class="bc-section-label">AI 做錯什麼</div>
      <div class="bc-cell-text">誤判修改範圍，把不該動的檔案也清空</div>
    </div>
    <div class="bc-cell">
      <div class="bc-section-label">人漏掉什麼</div>
      <div class="bc-cell-text">沒有在危險操作前設人工確認點</div>
    </div>
  </div>
  <div class="bc-defense" v-click>
    <div class="bc-section-label">防線</div>
    <div class="bc-defense-text"><code>PreToolUse</code> hook 攔截 delete、overwrite、recursive move、force push 等操作</div>
  </div>
  <div class="bc-rule" v-click>
    <span class="bc-rule-label">Rule 01</span>
    任何不可逆或大範圍操作，都不能讓 AI 自動通過
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 20 頁：Bad Case 2 -->

<div class="hook-eyebrow">團隊落地 · Bad Case 2</div>
<h1 class="hook-title bc-title">AI 自查是第一層，不是驗收</h1>

<div class="bc-wrap bc-sop">
  <div class="bc-trigger">
    <span class="bc-section-label">觸發情境</span>
    <span>AI 寫完後說「已檢查完成」，人直接送 PR</span>
  </div>
  <div class="bc-grid">
    <div class="bc-cell">
      <div class="bc-section-label">AI 做錯什麼</div>
      <div class="bc-cell-text">對自己剛寫的邏輯有盲點，漏掉邊界條件</div>
    </div>
    <div class="bc-cell">
      <div class="bc-section-label">人漏掉什麼</div>
      <div class="bc-cell-text">沒看 diff、沒跑測試、沒抽查核心流程</div>
    </div>
  </div>
  <div class="bc-defense" v-click>
    <div class="bc-section-label">防線</div>
    <div class="bc-defense-text">最低驗收：看 diff、跑測試、檢查關鍵路徑；必要時交叉 review</div>
  </div>
  <div class="bc-rule" v-click>
    <span class="bc-rule-label">Rule 02</span>
    AI 說完成不算完成，測試與人工驗收通過才算完成
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 21 頁：Bad Case 3 -->

<div class="hook-eyebrow">團隊落地 · Bad Case 3</div>
<h1 class="hook-title bc-title">Prompt 越模糊，AI 改動範圍越失控</h1>

<div class="bc-wrap bc-sop">
  <div class="bc-trigger">
    <span class="bc-section-label">觸發情境</span>
    <span>只描述「會錯」，但沒給錯誤訊息、方法名稱、重現步驟</span>
  </div>
  <div class="bc-grid">
    <div class="bc-cell">
      <div class="bc-section-label">AI 做錯什麼</div>
      <div class="bc-cell-text">為了保險，改了多個可能相關的地方</div>
    </div>
    <div class="bc-cell">
      <div class="bc-section-label">人漏掉什麼</div>
      <div class="bc-cell-text">沒有先界定問題邊界，也沒有要求 AI 先分析再改</div>
    </div>
  </div>
  <div class="bc-defense" v-click>
    <div class="bc-section-label">防線</div>
    <div class="bc-defense-text">Prompt 必須包含 class、method、error message、expected behavior、不可改區域</div>
  </div>
  <div class="bc-rule" v-click>
    <span class="bc-rule-label">Rule 03</span>
    沒有明確範圍的需求，只能進 Analyze，不能直接進 Coding
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- 第 22 頁：守則快覽 -->

<div class="hook-eyebrow">團隊落地</div>
<h1 class="hook-title">團隊 AI 開發 SOP</h1>

<div class="rules-wrap">
  <div class="rule-card">
    <span class="rule-num">01</span>
    <div class="rule-content">
      <div class="rule-title">危險操作必須人工確認</div>
      <div class="rule-desc">刪除、覆寫、大範圍搬移、force push、改設定檔，必須被 hook 或人工確認攔住</div>
    </div>
  </div>
  <div class="rule-card">
    <span class="rule-num">02</span>
    <div class="rule-content">
      <div class="rule-title">Plan 通過後才 Coding</div>
      <div class="rule-desc">AI 先說明影響範圍、修改策略、風險點；人確認後才進實作</div>
    </div>
  </div>
  <div class="rule-card">
    <span class="rule-num">03</span>
    <div class="rule-content">
      <div class="rule-title">模糊需求只做 Analyze</div>
      <div class="rule-desc">沒有錯誤訊息、重現步驟、目標行為，就不能讓 AI 直接寫 code</div>
    </div>
  </div>
  <div class="rule-card">
    <span class="rule-num">04</span>
    <div class="rule-content">
      <div class="rule-title">AI 自查不等於驗收</div>
      <div class="rule-desc">至少看 diff、跑測試、抽查核心流程；交叉 review 是多一道防線</div>
    </div>
  </div>
  <div class="rule-card">
    <span class="rule-num">05</span>
    <div class="rule-content">
      <div class="rule-title">PR Summary 只是草稿</div>
      <div class="rule-desc">AI 可以產初稿，送出前由人確認風險、測試結果與 reviewer 需要注意的點</div>
    </div>
  </div>
</div>

---
layout: default
class: content-slide hook-slide closing-flow-slide
---

<!-- 第 23 頁：結尾觀點 -->

<div class="hook-eyebrow">團隊落地</div>
<h1 class="hook-title">讓 AI 跟著你的流程走</h1>

<div class="closing-flow-wrap">
  <div class="closing-core">
    <div>真正有效的 AI 開發，不是找到最強的 Prompt，</div>
    <div>而是把自己的開發流程變成 AI 可以執行的 Skills。</div>
  </div>

  <div class="closing-points">
    <div class="closing-point">
      <span class="closing-point-num">01</span>
      <div>
        <div class="closing-point-title">把重複流程變成 Skill</div>
        <div class="closing-point-desc">Ticket 分析、Plan、Commit、PR、Code Review 都可以標準化</div>
      </div>
    </div>
    <div class="closing-point">
      <span class="closing-point-num">02</span>
      <div>
        <div class="closing-point-title">把團隊規則寫進 AI 流程</div>
        <div class="closing-point-desc">權限限制、Review 標準、測試要求，不靠每次人工提醒</div>
      </div>
    </div>
    <div class="closing-point">
      <span class="closing-point-num">03</span>
      <div>
        <div class="closing-point-title">讓 AI 成為流程的一部分</div>
        <div class="closing-point-desc">人負責判斷與驗收，AI 負責加速可重複的工作</div>
      </div>
    </div>
  </div>
</div>

---
layout: default
class: content-slide hook-slide
---

<!-- Next Step 頁：自學資源 -->

<div class="hook-eyebrow">團隊落地 · 下一步</div>
<h1 class="hook-title">想開始？帶走這些資源</h1>

<div class="resources-wrap">
  <div class="resources-col">
    <div class="resources-label">教學　從 0 開始</div>
    <a href="https://www.anthropic.com/learn" target="_blank" class="resources-item">
      <div class="resources-name">Anthropic Learn</div>
      <div class="resources-desc">官方學習中心　概念與應用情境</div>
    </a>
    <a href="https://code.claude.com/docs/zh-TW/quickstart" target="_blank" class="resources-item">
      <div class="resources-name">Claude Code 繁中文件</div>
      <div class="resources-desc">官方文件　從安裝到第一次使用</div>
    </a>
    <a href="https://claude.nagdy.me/learn/getting-started/" target="_blank" class="resources-item">
      <div class="resources-name">Getting Started · Nagdy</div>
      <div class="resources-desc">社群整理　搭配實例的入門路徑</div>
    </a>
  </div>
  <div class="resources-col">
    <div class="resources-label">Skill · 市集　看別人怎麼寫</div>
    <a href="https://skillsmp.com/" target="_blank" class="resources-item">
      <div class="resources-name">SkillsMP</div>
      <div class="resources-desc">Skill Marketplace　搜尋現成 skill</div>
    </a>
    <a href="https://www.aitmpl.com/" target="_blank" class="resources-item">
      <div class="resources-name">AI Templates</div>
      <div class="resources-desc">Skill / Prompt 模板庫</div>
    </a>
  </div>
  <div class="resources-col">
    <div class="resources-label">Skill · 推薦套件　我日常在用</div>
    <a href="https://github.com/affaan-m/everything-claude-code" target="_blank" class="resources-item">
      <div class="resources-name">everything-claude-code</div>
      <div class="resources-desc">本場 Demo 的 commit / prp-pr / code-review 都來自這</div>
    </a>
    <a href="https://github.com/obra/superpowers" target="_blank" class="resources-item">
      <div class="resources-name">superpowers</div>
      <div class="resources-desc">進階 skill 包　規劃、TDD、debugging</div>
    </a>
  </div>
</div>

<!--
說話點：
- 主管 / 想試的同事 → 從教學三條開始，半小時內能跑起來
- 想直接玩 Skill → 看市集，挑兩三個試
- 想複製我今天的流程 → 直接裝兩個推薦套件，照 SOP 跑
-->

---
layout: center
class: qa-slide
---

<!-- Q&A 頁 -->

<div class="qa-wrap">
  <div class="qa-marker">
    <span class="qa-marker-line"></span>
    <span class="qa-marker-label">Open · Discussion</span>
    <span class="qa-marker-line"></span>
  </div>

  <div class="qa-title-block">
    <h1 class="qa-title">Q<span class="qa-amp">&amp;</span>A</h1>
    <div class="qa-prompt">問方向、問流程、問踩雷案例都可以</div>
  </div>

  <div class="qa-ornament">
    <span class="qa-ornament-dot"></span>
    <span class="qa-ornament-dot qa-ornament-dot-mid"></span>
    <span class="qa-ornament-dot"></span>
  </div>

  <div class="qa-next-cue">Next · Scan slides</div>

  <div class="qa-foot">
    <span class="qa-foot-name">Vincent Yu</span>
    <span class="qa-foot-sep">·</span>
    <span class="qa-foot-dept">ACL_COE_MyA&amp;PRM</span>
  </div>
</div>

---
layout: center
class: ending-slide-new
---

<!-- 末頁 -->

<div class="ending-new-wrap">
  <div class="ending-new-copy">
    <div class="ending-new-kicker">Slides are available online</div>
    <div class="ending-new-title">Thank You.</div>
    <div class="ending-new-divider" />
    <div class="ending-new-subtitle">AI 輔助開發流程實戰</div>
    <div class="ending-new-url">gn870988.github.io/claude-code-in-action-slides</div>
    <div class="ending-new-meta">
      <span>Vincent Yu</span>
      <span>ACL_COE_MyA&amp;PRM</span>
      <span>2026</span>
    </div>
  </div>

  <div class="ending-new-qr-card">
    <div class="ending-new-qr-frame">
      <img src="/slides-qrcode.svg" class="ending-new-qr" alt="Slides QR code" />
    </div>
    <div class="ending-new-qr-label">Scan for slides</div>
  </div>
</div>
