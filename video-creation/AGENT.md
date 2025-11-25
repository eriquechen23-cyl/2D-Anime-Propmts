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

## 6. Advanced Narrative Schema (Act-Beat-Angle)
為確保高精度的影片生成，Prompt 必須包含以下三層結構資訊。

### [Level 1] Act {n} (敘事單元)
定義時間段落與整體氛圍。
* **Template**: `Act {n}（{t0–t1}s）`
* **Fields**:
    * `意圖`：{建立/敘事/情感/轉折/收束}
    * `視角策略`：{TPS (越肩) / Obari (大張透視) / POV / Bird's Eye} **(新增欄位)**
    * `美術要點`：{JJK Style/墨繪/暗黑/高對比}

### [Level 2] Beat {k} (動作節拍)
定義具體的表演與技術執行。
* **Template**: `Beat {k}（{t0–t1}s）`
* **Fields**:
    * `重點`：{情節/行為/情緒變化}
    * `Layout (分鏡佈局)`：
        * **必須明確定義前/中/後景**，例如：`[Fore: Weapon] -> [Mid: Hero] -> [Back: Ruins]`。
        * 若使用分鏡，標註 `Split Screen (Top/Bottom)`。
    * `Camera (運鏡技術)`：
        * 關鍵字：`Over-the-shoulder`, `Dolly Out`, `Push In`, `Dutch Angle`, `Foreshortening (透視變形)`.
    * `FX / Manga`：
        * **新增欄位**：專門描述漫畫特效。
        * 內容：`Screen Tone Overlay`, `Visualized Katakana SFX`, `Speed Lines`.
    * `光影`：{背光/輪廓光/體積光/眼神光}
    * `物理/質感`：{Ink Fluid (水墨流體) / Matte Painting (啞光)}

### [Level 3] Angle {a} (構圖規格)
* **Template**: `Angle {a}`
* **Fields**:
    * `構圖`：{三分線/中央/Z軸縱深/引導線}
    * `內容`：{特寫/越肩/敵人主觀/腳部特寫}
    * `安全`：{去Logo/去可讀字}