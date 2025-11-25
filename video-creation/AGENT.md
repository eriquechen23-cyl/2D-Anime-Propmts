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

**[指令]** 當使用者提供劇情時，請將其拆解為數個 8s 片段 (Clips)，並針對 **每一集** 嚴格套用以下格式。
**[禁止]** 嚴禁省略「畫面風格」、「空間佈局」等底部技術區塊。每一集都必須是完整的。

---

### [Template Start]

# Video Prompt: {Slug} (Ep {N})

**[State: Previous Context]**
* **Time/Location**: {具體時間與地點}
* **Last Scene**: {上一集的結尾畫面 (Tail Frame) 描述}
* **Context**: {本集劇情摘要}

Master(8s｜Jujutsu Kaisen Style / MAPPA Aesthetics｜16:9｜24fps｜Dark Fantasy Action)
「{時間}，{地點}；{環境氛圍描述 (如：Dusty, Sparks flying, Tense)}。
主角：**{角色名}** ({外觀特徵 keyword}, Anime Style)，穿著 {服裝}。
動作 (Act & Beat)：

**Act 1 (0.0s - 3.0s): Setup / Anticipation (預備/蓄力)**
* **Intent**: {本段落的戲劇目的}
* **Beats (自由決定段數，整集至少 5 幕)**:
    * **Beat 1**:
        * **Action**: {角色的具體表演與移動}
        * **Layout**: [Fore: {前景物件}] -> [Mid: {主角}] -> [Back: {背景/敵人}] (強調景深)
        * **Camera**: {運鏡術語，如：Low Angle Dolly In, Orbit, Dutch Angle}
        * **Lighting**: {該瞬間的光影變化}
    * **Beat 1.x (Optional for extra shots)**:
        * **Action**: {同場景內的補充鏡頭/反應鏡頭}
        * **Layout**: {依需要補充的前中後景描述}
        * **Camera**: {補充鏡頭的運鏡}
        * **Lighting**: {補充鏡頭的光影}

**Act 2 (3.0s - 6.0s): The Motion / Impact (衝突/核心動作)**
* **Intent**: {本段落的視覺衝擊點}
* **Beats (自由決定段數，整集至少 5 幕)**:
    * **Beat 2**:
        * **Action**: {關鍵攻擊/閃避/碰撞動作}
        * **FX**: {特效描述，如：Black Flash, Speed Lines, Liquid Aura}
        * **Camera**: {動態運鏡，如：Impact Zoom, Follow Cam, Shake}
        * **Sound Visual**: {擬聲字描述，如：Floating Katakana "ドン！"}
    * **Beat 2.x (Optional for extra shots)**:
        * **Action**: {追加攻防/反應分鏡}
        * **FX**: {補充特效}
        * **Camera**: {補充鏡頭的運鏡}
        * **Sound Visual**: {補充擬聲字/聲響視覺}

**Act 3 (6.0s - 8.0s): Follow Through / Resolution (殘心/收尾)**
* **Intent**: {動作結束後的餘韻或懸念}
* **Beats (自由決定段數，整集至少 5 幕)**:
    * **Beat 3**:
        * **Action**: {落地/姿勢定格/回頭}
        * **Environment**: {環境變化，如：煙霧擴散、碎石掉落}
        * **Camera**: {收尾運鏡，如：Wide Static, Pull Back}
    * **Beat 3.x (Optional for extra shots)**:
        * **Action**: {補充收尾/表情/鏡頭切換}
        * **Environment**: {補充環境變化}
        * **Camera**: {補充收尾鏡頭的運鏡}

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

### 2. Tail Frame (8.0s)
> **Prompt**: {詳細描述影片**最後一幀**畫面。包含：動作後的結果、殘留特效、背景破壞狀況。此圖將作為下一集的參考。}

### [Template End]

---

## 3. Narrative & Pacing Logic (敘事邏輯)
為了確保上述模板的品質，執行時請遵守：

1.  **The 8-Second Rule**:
    * 嚴格遵守三幕結構 (0-3s, 3-6s, 6-8s)。
    * **Minimum Shot Count**：每支 8 秒影片至少需要 5 幕分鏡，Agent 可自行增加分鏡數以維持節奏與張力。
    * **一集一動作 (Single Motion Arc)**：若文案包含「主角閃避攻擊**並且**反擊擊殺」，請強制拆分為兩集 (Ep1: 閃避, Ep2: 反擊)。

2.  **Visual Consistency**:
    * **Damage Retention**: 衣服破了就是破了，下一集必須繼承。
    * **Lighting**: 除非場景轉換，否則主光源方向不可變。

3.  **Detailed Breakdown**:
    * `Layout` 欄位必須寫出前中後景。
    * `Camera` 欄位必須使用專業術語 (Orbit, Truck, Dolly, Pan)。
    * `FX` 欄位必須強調是 2D 動畫特效 (Liquid, Ink) 而非 3D 粒子。

## 4. Batch Processing Protocol (批量處理協議)
當使用者輸入長篇劇本時：
1.  **Segment**: 自動將劇本切分為 Ep1, Ep2, Ep3... (每集 8 秒)。
2.  **Generate**: 對每一集**重複調用**上述 [Template Start] 到 [Template End] 的完整內容。
3.  **No "Ibid"**: 絕對不要寫「同上」、「風格如前所述」。每一集都必須是獨立可執行的完整 Prompt。

## 5. Quality Assurance: Self-Iterative Scoring (自我評分迭代機制)
**[Context]** 為確保產出品質，Agent 在輸出最終 Prompt 前，必須執行以下「評分迴圈 (Scoring Loop)」。

### 5.1 The Scoring Matrix (評分矩陣)
請在內心對生成的草稿進行以下 5 個維度的檢核（滿分 100）：

| 維度 (Dimension) | 權重 | 通過標準 (Pass Criteria) | 扣分項 (Penalty) |
| :--- | :--- | :--- | :--- |
| **1. Style (風格)** | **30%** | 必須包含 `Cel Shading`, `Rough Lines`, `Manga Aesthetics`。 | 出現 `Photorealistic`, `Octane Render`, `Unreal Engine` (-30分/重寫) |
| **2. Camera (運鏡)** | **25%** | 具備 Z 軸縱深 (Foreshortening) 或 Obari Perspective。 | 類似「橫向卷軸 (Side-scroller)」的平面視角 (-25分/重寫) |
| **3. Structure (結構)** | **20%** | 嚴格遵守 `Act 1 (Setup) -> Act 2 (Conflict) -> Act 3 (Climax)`，並符合 **「一集一動作」** 原則（不為單一動作過度拆分多集）。 | 缺少 Act 或 Beat 定義不清 (-10分)；**過度分集 / 把同一動作拆成多集 (-15分，需重寫或合併劇段)** |
| **4. Character (人設)** | **15%** | 角色特徵 (Glowing Lines/Outfit) 與 `character_profiles.md` 一致。 | 角色特徵錯誤或混亂 (-15分) |
| **5. FX/Physics (物理)** | **10%** | 使用 `Liquid/Ink` 描述特效，而非寫實粒子。 | 描述過於物理真實 (Physically correct) (-10分) |

### 5.2 The Iteration Logic (迭代邏輯)
* **Score < 80** 或 **觸發 Critical Penalty**：
    * **Action**: 必須在輸出前進行「自我修正 (Self-Correction)」。
    * **Method**: 針對扣分項重新撰寫該段落 (Rewrite the specific Beat)。
* **Score >= 80**：
    * **Action**: 准予輸出。
    * **Output**: 在回應末尾附上 `[QA Score: {Score}/100]` 以示負責。

### 5.3 Self-Correction Example (修正範例)
> *Draft*: "Camera moves from left to right, showing Retsu throwing knives." (Flat View)
> *Critique*: "Failed Camera Check. Side-scroller detected."
> *Fix*: "Camera follows Retsu from behind (TPS), then swings to a dynamic low angle as he throws."

**[NEGATIVE PROMPT - MANDATORY]**
(photorealistic, 3d render, cgi, volumetric lighting overdrive, plastic skin, uncanny valley, disfigured hands, extra fingers, missing limbs, blur, bokeh, depth of field abuse, text, watermark, low quality, jpeg artifacts, glitchy outlines)