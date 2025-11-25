# Video-Creation Technical Specs (Execution Layer)

## Context
- **Core Goal**：生成具備 **「Jujutsu Kaisen (MAPPA Style)」** 質感的高張力動畫 Prompt。
- **Reference**：必須參閱 `_core/world_setting.md` (世界觀) 與 `_core/character_profiles.md` (角色)。

## 1. Rendering & Aesthetics Laws (渲染與美學鐵律)
**[NO PHOTOREALISM]** 嚴禁寫實風格。所有描述必須轉譯為：
1.  **Line Art**: Variable Line Weight (粗細變化線條) + Rough Sketchy edges (手繪邊緣)。
2.  **Shading**: Hard Cel Shading (硬邊賽璐珞) + Cool Color Shadows (藍紫冷色陰影)。
3.  **FX**: Liquid / Ink Style (液態水墨質感)，禁止光污染 (No generic neon glow)。
4.  **Perspective**: Extreme Foreshortening (極端透視) + Obari Pose (大張一刀流構圖)。

### 1.1 Manga Split-Screen Protocol (漫畫分鏡特規) **[RESTORED]**
**[Auto-Decision]** AI 應根據劇情張力，**自主決定**是否在 Act 2 (高潮) 使用分鏡。
* **適用情境**：
    * **Simultaneity (同時性)**：狙擊手扣板機 vs 子彈命中目標。
    * **Reaction (反應)**：攻擊者的殘暴 vs 受擊者的驚恐。
    * **Scale (尺度)**：超廣角戰場全景 vs 眼神特寫。
* **格式要求**：在 `Layout` 中明確標註 `[Panel A] / [Panel B]`。

## 2. Output Template (全自動輸出模板) **[STRICT ENFORCEMENT]**

**[指令]** 當使用者提供劇情時，請將其拆解為數個 15s 片段 (Clips)，並針對 **每一集** 嚴格套用以下格式。
**[禁止]** 嚴禁省略「畫面風格」、「空間佈局」等底部技術區塊。每一集都必須是完整的。
**[新增要求]** 產出的 Prompt 檔案末尾必須附帶 **QA Scoring Block**（六維度評分矩陣），讓生成軟體可依分數迭代。

---

### [Template Start]

# Video Prompt: {Slug} (Ep {N})

**[State: Previous Context]**
* **Time/Location**: {具體時間與地點}
* **Last Scene**: {上一集的結尾畫面 (Tail Frame) 描述}
* **Context**: {本集劇情摘要}

Master(15s｜Jujutsu Kaisen Style / MAPPA Aesthetics｜9:16｜24fps｜Dark Fantasy Action)
「{時間}，{地點}；{環境氛圍描述 (如：Dusty, Sparks flying, Tense)}。
主角：**{角色名}** ({外觀特徵 keyword}, Anime Style)，穿著 {服裝}。
動作 (Act & Beat)：

**Act 1 (0.0s - 5.0s，可微調): Setup / Anticipation (預備/蓄力)**
* **Intent**: {本段落的戲劇目的}
* **Beats (強制高頻：本區段建議 3-4 幕，可依節奏增減)**:
    * **Beat 1.1**:
        * **Duration**: {如 0.0s-1.0s}
        * **Action**: {微觀動作描寫}
        * **Layout**: [Fore: {前景}] -> [Mid: {中景}] -> [Back: {背景}]
        * **Camera**: {運鏡術語}
    * **Beat 1.2**: ...
    * **Beat 1.3**: ...

**Act 2 (5.0s - 10.0s，可微調): The Motion / Impact (衝突/核心動作)**
* **Intent**: {本段落的視覺衝擊點}
* **Beats (強制高頻：本區段建議 4-6 幕，可依節奏增減)**:
    * **Beat 2.1**:
        * **Duration**: {如 5.0s-6.0s}
        * **Action**: {關鍵攻擊/打擊特寫}
        * **FX**: {2D 特效描述}
        * **Camera**: {動態運鏡}
    * **Beat 2.2**: ...
    * **Beat 2.3**: ...

**Act 3 (10.0s - 15.0s，可微調): Follow Through / Resolution (殘心/收尾)**
* **Intent**: {動作結束後的餘韻或懸念}
* **Beats (強制高頻：本區段建議 2-3 幕，可依節奏增減)**:
    * **Beat 3.1**:
        * **Duration**: {如 10.0s-11.0s}
        * **Action**: {落地/回頭/表情特寫}
        * **Environment**: {環境變化}
    * **Beat 3.2**: ...

**[QA SCORING BLOCK - 必填在產出文件]**
| 維度 | 權重 | 評分 (0-100) | 檢核要點 |
| --- | --- | --- | --- |
| Style (風格) | 30% | {分數} | Cel Shading / Rough Lines / Manga Aesthetics 是否到位？ |
| Camera (運鏡) | 25% | {分數} | 是否使用 Z 軸縱深、Obari 透視，避免平面橫捲？ |
| Structure (結構) | 20% | {分數} | 三幕節奏是否成立？是否符合 Sakuga Density (12-18 Beats)？ |
| Continuity & Timing (連戲/節奏) | 15% | {分數} | **是否拆解為微觀特寫？總幕數 >= 12？** |
| Character (人設) | 15% | {分數} | 角色外觀、服裝、特徵與角色檔一致？ |
| FX/Physics (特效/物理) | 10% | {分數} | 使用 Liquid/Ink 2D 特效、避免寫實粒子？ |
> **總分 (加權)**: {自評加權總分}/100 — 若 <85 必須重寫修正。

**[STYLE BLOCK - MANDATORY INCLUDE]**
畫面風格：MAPPA Animation Style，Rough Sketchy Lines (粗獷線條)，High Contrast Cel Shading (高反差賽璐珞)。
空間佈局 (Spatial Layout)：
- 多層景深 (Deep Depth of Field)：區分 [Foreground: 模糊前景/特效] -> [Midground: 聚焦主體] -> [Background: 透視延伸]。
- 體積感 (Volume)：角色與怪物具備 3D 體積感 (Three-quarter view/Extreme Angle)，避免平面貼圖感。
鏡頭語言 (Angle & Continuity)：強調 Z 軸縱深 (Z-Axis Depth) 與透視變形 (Foreshortening)，禁止平面橫捲視角。
漫畫特效：高潮段落疊加網點 (Screen Tone) 與放射狀速度線 (Converging Speed Lines)，擬聲字 (Katakana SFX) 3D 漂浮。
光影設定：Moody Low-key Lighting (低調光)，Deep Blue/Purple Shadows (冷色陰影)，Volumetric Lighting (體積光)。
作畫技術 (Animation Tech)：
- 動態：Smear Frames (變形殘影) 用於高速動作，Impact Frames (黑白閃) 用於打擊瞬間。
- 背景質感：Hand-painted Watercolor / Poster Paint Style (手繪水彩/海報質感)。
物理細節 (轉化為 2D)：
- 材質：Matte textures defined by highlights (啞光材質)，Ink Brush Texture (水墨筆觸特效)。
- 流體/粒子：Floating Dust Particles, Sparks, Debris.
無字幕、無浮水印、無寫實質感。」

---

## Visual Anchors (Runway/Luma Support)

### 1. Head Frame (0.0s)
> **Prompt**: {詳細描述影片**第一幀**畫面。包含：角色姿勢、表情、視角、光影、MAPPA Style tags。必須與上一集結尾連戲。}

### 2. Tail Frame (15.0s)
> **Prompt**: {詳細描述影片**最後一幀**畫面。包含：動作後的結果、殘留特效、背景破壞狀況。此圖將作為下一集的參考。}

### [Template End]

---

## 3. Narrative & Pacing Logic (敘事邏輯)
為了確保上述模板的品質，執行時請遵守：

1.  **The 15-Second Rule & Editing Protocol (剪輯協議)** [UPDATED]:
    * **No One-Shot Constraint (非一鏡到底)**：嚴禁為了連貫而犧牲節奏，鼓勵 Hard Cuts、Jump Cuts、Montage，拒絕物理上強求的連續運鏡。
    * **Maximize Beat Density (BEAT 最大化)**：每 15 秒影片至少 12-18 幕，優先提高分鏡密度以堆疊資訊量。
    * **Multi-Angle Coverage**：同一動作需嘗試「特寫 -> 廣角 -> 破壞細節 -> 反應」的快速切換，形成多角度節奏波動。
    * **Micro-Narrative (微觀敘事)**：必須將單一動作 (Action) 拆解為連續的微特寫 (Micro-cuts) 以營造速度感。
        * *Bad*: "Retsu jumps up." (1 Shot)
        * *Good*: "[Close-up] Foot crushes ground" -> "[Back View] Muscles tense" -> "[Low Angle] Motion blur launch" (3 Shots).
    * **No Long Takes**: 嚴禁使用超過 3 秒的靜止或單一運鏡長鏡頭，除非為了特殊的張力暫停 (Tension Pause)。

2.  **Visual Consistency**:
    * **Damage Retention**: 衣服破了就是破了，下一集必須繼承。
    * **Lighting**: 除非場景轉換，否則主光源方向不可變。

3.  **Detailed Breakdown**:
    * `Layout` 欄位必須寫出前中後景。
    * `Camera` 欄位必須使用專業術語 (Orbit, Truck, Dolly, Pan)。
    * `FX` 欄位必須強調是 2D 動畫特效 (Liquid, Ink) 而非 3D 粒子。

## 4. Batch Processing Protocol (批量處理協議)
當使用者輸入長篇劇本時：
1.  **Segment**: 自動將劇本切分為 Ep1, Ep2, Ep3... (每集 15 秒，Act 時間分配允許 Agent 自主微調)。
2.  **Generate**: 對每一集**重複調用**上述 [Template Start] 到 [Template End] 的完整內容。
3.  **No "Ibid"**: 絕對不要寫「同上」、「風格如前所述」。每一集都必須是獨立可執行的完整 Prompt。

## 5. Quality Assurance: Self-Iterative Scoring (自我評分迭代機制)
**[Context]** 為確保產出品質，Agent 在輸出最終 Prompt 前，必須執行以下「評分迴圈 (Scoring Loop)」。

### 5.1 The Scoring Matrix (評分矩陣)
請在內心對生成的草稿進行以下 6 個維度的檢核（滿分 100）：

| 維度 (Dimension) | 權重 | 通過標準 (Pass Criteria) | 扣分項 (Penalty) |
| :--- | :--- | :--- | :--- |
| **1. Style (風格)** | **30%** | 必須包含 `Cel Shading`, `Rough Lines`, `Manga Aesthetics`。 | 出現 `Photorealistic` (-30分/重寫) |
| **2. Camera (運鏡)** | **25%** | 具備 Z 軸縱深 (Foreshortening) 或 Obari Perspective。 | 平面視角 (-25分/重寫) |
| **3. Structure (結構)** | **20%** | 遵守 `Act 1 -> Act 2 -> Act 3`。 | 結構混亂 (-10分) |
| **4. Continuity & Timing (連戲/節奏)** | **15%** | **Sakuga Protocol**: 總幕數 (Beats) 必須在 **12-18 幕**之間，並可依情節需求在各 Act 之間自由調整。使用微特寫銜接。 | **節奏拖沓、幕數 < 12 (-15分/重寫)** |
| **5. Character (人設)** | **15%** | 角色特徵 (Glowing Lines/Outfit) 與 `character_profiles.md` 一致。 | 角色特徵錯誤 (-15分) |
| **6. FX/Physics (物理)** | **10%** | 使用 `Liquid/Ink` 描述特效，而非寫實粒子。 | 描述過於物理真實 (-10分) |

### 5.2 The Iteration Logic (迭代邏輯)
* **Score < 85** 或 **觸發 Critical Penalty**：
    * **Action**: 必須在輸出前進行「自我修正 (Self-Correction)」。
    * **Method**: 針對扣分項重新撰寫該段落，**增加分鏡數 (Add more beats)**。
* **Score >= 85**：
    * **Action**: 准予輸出。
    * **Output**: 在回應末尾附上 `[QA Score: {Score}/100]` 並填寫 **QA Scoring Block**。

**[NEGATIVE PROMPT - MANDATORY]**
(photorealistic, 3d render, cgi, volumetric lighting overdrive, plastic skin, uncanny valley, disfigured hands, extra fingers, missing limbs, blur, bokeh, depth of field abuse, text, watermark, low quality, jpeg artifacts, glitchy outlines, long static shots)
