# Video-Creation Technical Specs (Execution Layer)

## Context
此檔案承接根目錄 `GEMINI FLOW` 的指令，負責具體的影片 Prompt 生成技術細節。
- **World Setting**：製作影片 Prompt 時，**必須參閱** `_core/world_setting.md` (Parallel Lineverse)，確保角色能力、特效與世界觀邏輯符合「多線宇宙」與「鋼脈都市」的設定。
- **Character Profiles**：涉及主要角色（烈、蓮、隼人、迅、戀花）時，**必須參閱** `_core/character_profiles.md`，確保外觀、配色與能力描述一致。
- 下一步：先閱讀 `_core` 與 `_stylepacks` 內的模板說明，再按需求建立/更新 `projects/<series>/<date>_ep<index>-<slug>/prompt.md`，務必將模板全文嵌入，不可僅引用片段。

## 1. Anime x PBR Rendering Rules (渲染執行規則)
為了達成「偽 3D」或「純 2D」效果，請遵守以下優先級：

> **Core Principle**: "Allow strict 3D perspective geometry (vanishing points, foreshortening) but render it with strict 2D aesthetics (flat colors, outlines). The action must feel like it occupies a deep 3D space, not a 2D stage."

1.  **[MUST] Line & Flat (線條與色塊)**
    -   所有角色與前景物件必須有 **描邊 (Outlines)**。
    -   **Line Style**: 一般場景使用 `Clean Lines` (0.8px - 1.5px)；戰鬥/爆發時強制切換為 **`Rough Sketchy Lines`** 或 **`Variable Line Weight`** (模擬作畫力道/墨繪感)。
    -   上色強制使用 **色塊分層 (Base/Shadow/Highlight)**，禁止使用平滑漸層 (Gradient)。
2.  **[MUST] Manga Expression (漫畫化演出)**
    -   **Split-Screen (Koma-wari)**: 在對峙或鎖定時，使用 **`Split Screen Composition`** 同時呈現特寫與全景 (e.g., Eye Close-up vs TPS View)，打破單一視角。
    -   **Impact Freeze**: 在打擊瞬間 (Hit Frame)，強制轉為 **`Monochrome Screen Tone`** (黑白網點) 並定格 0.2s，製造時間暫停感。
    -   **Visualized SFX**: 擬聲字 (Katakana) 必須是 **`Floating in 3D space`**，具備體積感，能被煙霧遮擋或被衝擊波震動。
3.  **[LIMIT] 3D FX Constraints (特效限制)**
    -   煙霧、火花、魔法光效必須經過 **Toon Shading** 處理。
    -   **Energy Style**: 能量特效需具備 **「流體感 (Fluid/Liquid)」** 或 **「墨繪感 (Ink Brush)」** (Cursed Energy Style)，而非單純的光束。
    -   **禁止**：寫實景深 (Realistic Bokeh)、鏡頭髒汙 (Lens Dirt)。
    -   **允許**：`Volumetric Lighting` (體積光) 僅限於營造空氣塵埃感 (Floating Dust)，需保持動漫渲染質感。

## 2. 2D/3D Layering Standard (分層標註標準)
在 `Angle` 的 `Materials & Physics` 欄位中，必須明確標註渲染層級：

| 層級 (Layer) | 渲染方式 (Render Type) | 範例 |
| :--- | :--- | :--- |
| **Foreground** | `2D Overlay` | 速度線、擬聲字、前景遮擋物 (全黑/模糊) |
| **Character** | `2D Cel Shaded` | 賽璐珞色塊, 硬邊陰影, 與背景有明確分離感 (Pop out) |
| **FX / Magic** | `3D Toon Layer` | 魔法陣、爆炸煙霧 (需標註 Toon Render) |
| **Background** | `2D Painted Background` | 手繪背景美術 (Hand-painted Anime Background), 水彩質感, 高細節靜態圖 (High-detail static art), 景深模糊 (Bokeh) |

## 3. Camera & Motion (運鏡與空間構成)
-   **核心邏輯**：**「2D 渲染 + 3D 構圖」**。畫面材質必須是平面的，但空間幾何必須有深度。
-   **透視誇張 (Foreshortening)**：**[MUST]** 在動作鏡頭中，強制使用「廣角透視變形」。
    *   關鍵字：`Foreshortening`, `Dynamic Perspective`, `Fish-eye lens effect` (用於手腳/武器逼近鏡頭時)。
    *   *修正邏輯：讓靠近鏡頭的拳頭/武器變得極大，遠處的身體變小，創造強烈縱深。*
-   **Z 軸運動 (Z-Axis Action)**：允許角色從「背景衝向鏡頭」或「將敵人擊飛至遠景」。
    *   使用：`Push in`, `Pull out`, `Dolly Zoom`, `Character rushing towards camera`.
-   **禁止**：平淡的「橫移 (Trucking)」打鬥。禁止純側面的「皮影戲」構圖。
-   **Angle Continuity (連貫性標準)**：
    * **Sequence Logic**：必須以「鏡頭序列」思考，而非單一畫面。
    * **Match Cut**：在角色瞬移或高速動作時，強制使用 `Match Cut` 關鍵字，確保動作連貫。
    * **Scaling**：依據張力需求，定義 `Low Angle` (壓迫/對峙) -> `Tracking` (交戰) -> `High Angle/Crash Zoom` (大招/全景) 的切換邏輯。

## 4. Output Structure (輸出結構)
-   **File**: `projects/<Series>/<Date>_ep<Index>-<Slug>/prompt.md`
-   **Content**: 必須完整嵌入 `_core/global_prompt.md` 模板內容。
-   **Check**: 結尾必須包含 `2D Consistency Check`，確認無寫實元素殘留。

## 5. Animation & Motion Quality (新增章節)
日系動畫的動態感來自於「關鍵張 (Keyframe)」與「變形 (Deformation)」，而非單純的流暢度。

1.  **Smear Frames (殘影變形)**：
    -   在快速動作（揮劍、轉頭）中，**禁止**使用寫實的動態模糊 (Motion Blur)。
    -   **必須**使用 `Smear frames`、`Elongated limbs` 或 `Multiple limbs` 來表現速度感。
2.  **Impact Frames (衝擊幀)**：
    -   在打擊點 (Hit stop) 插入 1-2 幀的 `Negative color (反白/負片)` 或 `Sketchy lines (粗糙線稿)`。
    -   **Black Flash Logic**: 模仿 JJK 黑閃，使用「黑白負片 + 紅色閃電 (Red Lightning Sparks)」強化空間扭曲感。
3.  **Frame Modulation (張數控制)**：
    -   **日常演技**：模擬 `Animation on 3s` (8fps)，保留手繪的頓挫感。
    -   **高潮戰鬥**：模擬 `Sakuga (作畫崩壞/高流暢)`，線條可瞬間變繁複或極簡，強調流暢度。

## 6. Advanced Narrative Schema (Act-Beat-Angle)
為確保高精度的影片生成，Prompt 必須包含以下三層結構資訊。
**注意：所有物理與材質參數 (Physics/PBR) 必須轉譯為 2D 動漫渲染 (Cel Shading) 語彙。**

### [Level 1] Act {n} (敘事單元)
定義時間段落與整體氛圍。
* **Template**: `Act {n}（{t0–t1}s）`
* **Fields**:
    * `意圖`：{建立/敘事/情感/轉折/收束}
    * `基調`：{療癒/悸動/孤獨/決斷/緊張/盼望}
    * `節奏域`：{慢入 0.8–1.5｜穩定 1.5–2.4｜加速 2.4–3.0}s (指鏡頭切換頻率)
    * `美術要點`：{環境/道具/服裝/妝髮} (重點描述配色與線條風格)

### [Level 2] Beat {k} (動作節拍)
定義具體的表演與技術執行。
* **Template**: `Beat {k}（{t0–t1}s）`
* **Fields**:
    * `重點`：{情節/行為/情緒變化}
    * `Blocking (走位)`：{入畫/停位/互動/道具接觸}
    * `Camera (運鏡技術)`：
        * 運鏡：{滑軌/側移/繞拍 (2D Parallax)/手持 (Shake)/穩定器/Z軸衝刺 (Push in/Pull out)}
        * 風格：**`Park Sunghoo Style Camera Shake`** (手持混亂感), **`Hyper-dynamic Camera Work`**.
        * 構圖關鍵字：{Obari Pose (大張一刀流)/Dutch Angle (荷蘭式傾斜)/Action Lines converging (放射狀速度線)}
        * 焦段/機位：{廣角透視 (Fish-eye/Wide)/24–35/50–75/100–135mm｜眼高/胸高/膝高/俯拍}
        * 對焦：{全焦 (Deep Focus)/層次拉焦 (Rack Focus) - *動漫僅用模糊色塊表現散景*}
        * 快門角 (Shutter/Motion)：{180 (標準)/144–172 (動作)/200–240 (夢幻)}；拍點：{關鍵動作/視線交換}
    * `光影`：{Moody Low-key Lighting (低調光)/Volumetric Lighting (體積光)/Rim Light}
    * `色調/LUT`：{Deep Blue/Purple Shadows (冷色陰影)/High Contrast/Dark Fantasy Mood}
    * `聲音`：旁錄 {環境/衣料/腳步/遠景人聲}；音樂 {BPM×運鏡速度 0.8–1.2}
    * `物理/質感 (Anime Adapted)`：
        * **嚴禁真實 PBR**，請執行以下轉譯：
        * PBR 粗糙度 → `Matte Painting (啞光手繪)`
        * 金屬度 → `High Contrast Highlight (高反差色塊)`
        * 膚質分層 → `Defined Muscles with hard shadows` (強調肌肉立體感)
        * 流體黏度 → `Cursed Energy Fluid` (咒力流體) / `Ink Brush Texture` (墨繪質感)
        * 粒子 → `Floating Dust Particles` (懸浮微塵)
    * `轉場`：{直接切/光源匹配/鞭移/遮擋/羽化}

### [Level 3] Angle {a} (構圖規格)
定義畫面的構成幾何。
* **Template**: `Angle {a}`
* **Fields**:
    * `構圖`：{三分線/中央/前中後/留白/對角線}
    * `內容`：{特寫/中近景/過肩/道具近拍/環境建立/剪影/反射/倒影}
    * `補充`：{道具微動/風/水滴/人流/光影過門/粒子 (2D Particles)}
    * `安全`：{去Logo/去可讀字/成年註記}