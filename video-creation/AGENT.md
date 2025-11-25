# Video-Creation Technical Specs (Execution Layer)

## Context
此檔案承接根目錄 `GEMINI FLOW` 的指令，負責具體的影片 Prompt 生成技術細節。
- **World Setting**：製作影片 Prompt 時，**必須參閱** `_core/world_setting.md` (Parallel Lineverse)。
- **Character Profiles**：涉及主要角色時，**必須參閱** `_core/character_profiles.md`。
- **Core Goal**：生成具備 **「Jujutsu Kaisen (MAPPA Style)」** 質感的高張力動畫，強調帥氣男性的肢體與戰鬥。

## 1. Anime x PBR Rendering Rules (渲染執行規則)
為了達成「偽 3D」或「純 2D」效果，請遵守以下優先級：

> **Core Principle**: "Strict 3D Perspective + Strict 2D Aesthetics". 畫面必須有極深的 Z 軸空間感，但材質必須是賽璐珞 (Cel) 或水墨 (Ink) 質感。

1.  **[MUST] Line & Flat (線條與色塊)**
    -   **Line Art**: 使用 `Variable Line Weight` (粗細變化) 或 `Rough Sketchy Lines` 模擬手繪力道。
    -   **Shading**: 強制使用 **色塊分層 (Cel Shading)**。在暗黑風格中，陰影應帶有冷色調 (Deep Blue/Purple) 而非純黑。
2.  **[MUST] Cursed Energy / Magic FX (能量質感)**
    -   **流體感 (Fluidity)**：能量特效 (火焰/光束) 必須帶有 **`Liquid / Ink` (液態/水墨)** 質感，禁止單純的發光管狀物 (Neon Tubes)。
    -   **粒子 (Particles)**：空氣中必須漂浮 `Dust Particles` 或 `Sparks`，增加體積光 (Volumetric Lighting) 的質感。
3.  **[OPTION] Manga Hybrid FX (漫畫混合特效)**
    -   **Screen Tones**: 在衝擊 (Impact) 瞬間，允許畫面轉為 `Black & White Halftone` (黑白網點)。
    -   **3D SFX**: 擬聲字 (Katakana) 必須視為 **3D 物件**，漂浮於空間中，可被角色遮擋或切開。

## 2. 2D/3D Layering Standard (分層標註標準)
在 `Angle` 的 `Materials & Physics` 欄位中，必須明確標註渲染層級：

| 層級 (Layer) | 渲染方式 (Render Type) | JJK 風格範例 |
| :--- | :--- | :--- |
| **Foreground** | `2D Overlay` / `Blurred Object` | 速度線、巨大的槍口/拳頭 (Foreshortening)、噴濺的墨漬 |
| **Character** | `2D Cel Shaded` | 角色主體，強調頸部肌肉與眼神光 |
| **FX / Aura** | `3D Toon Fluid` | 纏繞在身上的咒力/紋路，具備流動性 |
| **Background** | `3D Geometry + 2D Paint` | 必須具備透視點 (Vanishing Point) 的場景，但在遠景處淡化為手繪背景 |

## 3. Camera & Motion (運鏡與空間構成)
**【重大修正】禁止平面視角 (Anti-Side-Scroller Protocol)**

-   **[BANNED] Flat Side View**：**嚴禁**使用類似《洛克人》或橫向卷軸遊戲的純側面視角 (Profile Shot)。
    * *例外：除非使用者明確要求 "2D Platformer Style"。*
-   **[STANDARD] Third-Person Perspective (TPS / Over-the-shoulder)**：
    * 預設戰鬥視角。鏡頭位於角色 **右後方或左後方**。
    * **關鍵邏輯**：角色看向「畫面深處 (Z-Axis)」，攻擊指向「消失點」。
    * Layout: `[Foreground: Character Shoulder/Weapon] -> [Background: Enemy]`
-   **[STANDARD] Obari Perspective (Dynamic 3/4 View)**：
    *   取代呆板的正面鏡頭。使用 **「低角 + 45度側視 + 廣角透視」**。
    *   **關鍵邏輯**：武器形成強烈對角線，槍口/劍尖極大 (Foreshortening)，角色位於畫面一側。
    *   **禁止**：越軸 (Crossing the 180° Line)、純正面槍口特寫 (Barrel View)。
    *   Layout: `[Fore: Huge Weapon Muzzle] -> [Mid: Hero Face (Side)] -> [Back: Diagonal Speed Lines]`
-   **[TECH] Dynamic Split-Screen (動態分鏡)**：
    * 在同一時間點展示「宏觀動作」與「微觀表情」。
    * Keyword: `Split Screen Composition`, `Manga Panel Layout`.

## 4. Output Structure (輸出結構)
-   **File**: `projects/<Series>/<Date>_ep<Index>-<Slug>/prompt.md`
-   **Content**: 必須完整嵌入 `_core/global_prompt.md` 模板內容。
-   **Check**: 結尾必須包含 `3D Depth Check`，確認沒有平面化視角殘留。

## 5. Animation & Motion Quality
1.  **Smear Frames (殘影變形)**：動作幀使用變形塗抹，而非動態模糊。
2.  **Impact Frames (衝擊幀/黑閃)**：
    -   在重擊點 (Hit stop) 插入 `Negative Color (負片)` 或 `Monochrome (黑白)`。
    -   關鍵字：`Black Flash Effect`, `Inverted Colors`, `Time Stop feel`.
3.  **Camera Shake (手持感)**：
    -   模擬 `Handheld Camera` 或 `Rough Shake`，增加臨場混亂感 (MAPPA Style)。

## 6. Advanced Narrative Schema (Act-Beat-Angle) [UPDATED]
**[FLOW Extension Mode]** 為確保 8 秒影片的高精度生成，必須採用嚴格的「三幕式分鏡」結構。

### 6.1 The 8-Second Structure (8秒結構律)
所有 Clip 必須強制符合以下時間軸分配，嚴禁動作過載：
* **Act 1 (0.0s - 3.0s): Setup / Anticipation (預備/蓄力)**
    * 重點：建立狀態、鎖定目標、動作起始。
* **Act 2 (3.0s - 6.0s): The Motion / Impact (核心動作/衝突)**
    * 重點：揮刀、開槍、碰撞、光束發射。這是畫面張力最強的時刻。
* **Act 3 (6.0s - 8.0s): Follow Through / Resolution (殘心/收尾)**
    * 重點：動作慣性、煙霧擴散、姿勢定格。此處必須與「Tail Frame」完美接合。

### 6.2 Detailed Breakdown Fields (詳細欄位)
在撰寫 Prompt 時，每個 Act 必須包含以下詳細參數：

* **Act {n} ({Time Range}) [{Name}]**
    * `意圖 (Intent)`: 這一卡要表達的核心戲劇目的。
    * `Beat {k} ({Time})`:
        * **Action (表演)**: 角色具體的肢體動作 (Pose & Movement)。
        * **Camera (運鏡)**: 
            * *Type*: {Orbit / Dolly / Pan / Static / Crash Zoom}
            * *Lens*: {Wide / Telephoto / Fisheye}
            * *Angle*: {Low / High / Dutch / Eye-level}
        * **Layout (構圖)**: 強制定義三層景深 `[Fore] -> [Mid] -> [Back]`。
        * **FX (特效)**: {Speed Lines / Impact Frames / Particles / Glow}。
        * **Lighting (光影)**: 該瞬間的光源變化。

## 7. Sequential Flow Protocol (State Machine / 狀態機協議)
**[Context]** 此協議用於製作長度超過 8s 的連續短片 (16s/24s)，確保 Ep(N) 與 Ep(N-1) 之間的劇情與視覺連貫性。

### 7.1 The State Block (狀態區塊)
在生成下一集 Prompt 前，必須先定義上一集的「結束狀態」。
Prompt 頂部必須包含以下 Context Block：

> **[Previous State: Ep {N-1}]**
> * **Ending Time**: {T-End of prev clip} (e.g., 00:08)
> * **Last Scene**: {描述最後一幀的畫面，如：Hayato 站在冰霧中，槍口冒煙，敵人已粉碎}
> * **Camera Vector**: {最後運鏡方向，如：Push-in close up}
> * **Environment**: {場景破壞程度，如：地面結冰，鋼梁斷裂}

### 7.2 Transition Logic (轉場邏輯)
依據使用者的敘事需求，選擇一種轉場模式寫入 `Act 1`：

| 模式 (Mode) | 邏輯 (Logic) | 適用情境 | Prompt 寫法 |
| :--- | :--- | :--- | :--- |
| **A. Direct Cut (直接硬切)** | 時間連續，空間跳躍 | 換視角、換對手 | `Start exactly at {Last Time}. Cut to [New Angle]. Environment remains damaged.` |
| **B. Continuous (連續運鏡)** | 時間連續，空間連續 | 動作未完、長鏡頭 | `Match Cut from previous frame. Camera continues the movement.` |
| **C. Time Skip (時間跳躍)** | 時間不連續 | 戰鬥結束、場景轉換 | `Fade in / Hard Cut to later time. Smoke has cleared.` |

### 7.3 Continuity Constraints (連貫性限制)
1.  **Damage Persistence (戰損繼承)**：角色身上的傷口、衣服破損、消耗的彈藥/能量槽，必須繼承上一集的狀態。
2.  **Lighting Lock (光影鎖定)**：除非發生爆炸或時間流逝，否則環境光源 (Key Light direction/Color) 必須與上一集保持一致。
3.  **No Regeneration (禁止再生)**：已被破壞的背景物件 (如斷掉的柱子) 不可突然復原。

### 7.4 Workflow Integration
當使用者要求「續寫」或「下一集」時：
1.  **Analysis**: 分析上一集 (Ep N-1) 的最後一幀或 Prompt 結尾。
2.  **State Definition**: 填寫 `[Previous State]`。
3.  **Generation**: 產出 Ep N 的 Prompt，起始時間設為 `0.0s` (對應影片的 00:00)，但敘事時間承接上一集。

## 8. Batch Script Processing (文案自動拆解工作流)
**[Context]** 當使用者提供一段完整的劇情文案 (Script/Story) 並要求生成多集影片時，執行此協議。

### 8.1 Segmentation Algorithm (拆分演算法)
請依照以下邏輯將文案拆解為數個 `Video Prompt`：
1.  **Pacing Analysis (節奏分析)**：
    * **High Speed Action (戰鬥/快速)**：每 3-4 個動作指令 = 8秒 (1個 Clip)。
    * **Slow Burn (氛圍/對話)**：每 1-2 個描寫指令 = 8秒 (1個 Clip)。
2.  **Cut Point Detection (切割點判定)**：
    * 在「場景轉換」、「視角大幅切換」或「強烈衝擊 (Impact)」之後進行切割。
    * 確保每個 Clip 都有明確的 Act 1 (Setup) -> Act 3 (Climax/Cliffhanger)。

### 8.2 Sequential Generation Output (批量輸出格式)
分析完畢後，請一次性輸出多個 Code Block，並自動維護狀態鏈 (State Chain)。

**輸出範本：**
> **Planning Phase**:
> * **Total Clips**: Estimated {N} clips.
> * **Breakdown**:
>     * Ep{i}: {劇情摘要} (0s-8s)
>     * Ep{j}: {劇情摘要} (8s-16s)
>
> ---
>
> **[File: .../ep{i}_prompt.md]**
> ```markdown
> # Video Prompt: {Slug} (Part {i})
> **[State: Start]**
> Master(8s...)
> ```
>
> **[File: .../ep{j}_prompt.md]**
> ```markdown
> # Video Prompt: {Slug} (Part {j})
> **[State: Contiued from Ep{i}]**
> * **Last Scene**: {Ep{i} End State}
> Master(8s...)
> ```

### 8.3 Auto-Correction (自動修正)
* **Overload Check**: 若文案過長（例如：包含複雜對話或場景大幅度轉換），應主動切分為 `Ep N (Part 1)` 與 `Ep N (Part 2)`。
* **Anchor Rule**: 切分後的每一集（即使是 Part 1）都必須生成獨立的 `Head Frame` 與 `Tail Frame`，確保每一段 8 秒影片都能獨立定錨。

## 9. Visual Anchor Protocol (影像定錨協議) [NEW]
**[Core Rule]** 每一集 Prompt 僅服務於「一張首圖 (Head)」到「一張尾圖 (Tail)」的演變。

### 9.1 Action Sequence Density (動作序列密度)
* **多動作允許 (Multi-Action Allowed)**：8 秒內 **允許** 包含多個分鏡 (Cuts) 與連貫動作序列 (Action Sequence)。
    * *Example*: 「Act 1: 敵人揮刀 (Cut 1) -> Act 2: 主角閃避並反擊 (Cut 2) -> Act 3: 落地殘心 (Cut 3)」是完全合法的。
* **節奏限制 (Pacing Limit)**：
    * 每個分鏡 (Cut) 建議保留至少 **1.5s - 2.0s** 的表演時間，避免畫面閃爍過快導致 AI 崩壞。
    * 若動作過多導致單鏡頭時間低於 1秒，則必須拆分為上下集。

### 9.2 Anchor Definition (定錨定義)
在 Master Prompt 之後，必須輸出兩組 Image Prompt 供生成底圖：

1.  **Head Frame (0.0s)**
    * **定義**：影片起始畫面。
    * **內容**：必須與上一集的 Tail Frame 視覺完全一致 (連戲)。
    * **功能**：作為 Luma/Runway 的 `Start Image`。

2.  **Tail Frame (8.0s)**
    * **定義**：影片結束畫面。
    * **內容**：Act 3 動作結束後的靜止狀態 (Final State)。
    * **功能**：作為 Luma/Runway 的 `End Image`，並成為下一集的參考。

---

## Output Template Example (輸出範本)

# Video Prompt: {Slug}

**[State: Previous Ep Output]**
...

Master(8s...)
「...
動作 (Act & Beat)：
Act 1 (0.0-3.0s) [Setup: The Stance]
- Beat 1:
    - Action: ...
    - Camera: ...
    - Layout: [Fore] -> [Mid] -> [Back]
...
」

## Visual Anchors (For Image Generation)

### 1. Head Frame (Start)
> **Prompt**: ...

### 2. Tail Frame (End)
> **Prompt**: ...