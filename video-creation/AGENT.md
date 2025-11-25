# Video-Creation Technical Specs (Execution Layer)

## Context
此檔案承接根目錄 `GEMINI FLOW` 的指令，負責具體的影片 Prompt 生成技術細節。
- **World Setting**：製作影片 Prompt 時，**必須參閱** `_core/world_setting.md` (Parallel Lineverse)，確保角色能力、特效與世界觀邏輯符合「多線宇宙」與「鋼脈都市」的設定。
- **Character Profiles**：涉及主要角色（烈、蓮、隼人、迅、戀花）時，**必須參閱** `_core/character_profiles.md`，確保外觀、配色與能力描述一致。
- 下一步：先閱讀 `_core` 與 `_stylepacks` 內的模板說明，再按需求建立/更新 `projects/<series>/<date>_ep<index>-<slug>/prompt.md`，務必將模板全文嵌入，不可僅引用片段。

## 1. Anime x PBR Rendering Rules (渲染執行規則)
為了達成「偽 3D」或「純 2D」效果，請遵守以下優先級：

1.  **[MUST] Line & Flat (線條與色塊)**
    -   所有角色與前景物件必須有 **描邊 (Outlines)** (0.8px - 1.5px)。
    -   上色強制使用 **色塊分層 (Base/Shadow/Highlight)**，禁止使用平滑漸層 (Gradient)。
2.  **[MUST] Manga Expression (漫畫化演出)**
    -   在高潮 (Climax) 或衝擊 (Impact) 鏡頭，強制疊加 **網點 (Screen Tone)**、**速度線 (Speed Lines)** 與 **擬聲字 (Katakana SFX)**。
3.  **[LIMIT] 3D FX Constraints (特效限制)**
    -   煙霧、火花、魔法光效必須經過 **Toon Shading** 處理。
    -   **禁止**：真實體積光 (Volumetric Fog)、寫實景深 (Realistic Bokeh)、鏡頭髒汙 (Lens Dirt)。

## 2. 2D/3D Layering Standard (分層標註標準)
在 `Angle` 的 `Materials & Physics` 欄位中，必須明確標註渲染層級：

| 層級 (Layer) | 渲染方式 (Render Type) | 範例 |
| :--- | :--- | :--- |
| **Foreground** | `2D Overlay` | 速度線、擬聲字、前景遮擋物 (全黑/模糊) |
| **Character** | `2D Cel Shaded` | 賽璐珞色塊, 硬邊陰影, 與背景有明確分離感 (Pop out) |
| **FX / Magic** | `3D Toon Layer` | 魔法陣、爆炸煙霧 (需標註 Toon Render) |
| **Background** | `2D Painted Background` | 手繪背景美術 (Hand-painted Anime Background), 水彩質感, 高細節靜態圖 (High-detail static art), 景深模糊 (Bokeh) |

## 3. Camera & Motion (運鏡限制)
-   **焦段**：鎖定 24mm / 35mm / 50mm / 85mm。
-   **運鏡**：以 **平移 (Truck/Dolly)** 為主，模擬傳統動畫攝影台 (Multi-plane Camera) 效果。
-   **禁止**：360 度繞拍 (Orbit)、極端魚眼、不自然的 Z 軸穿梭。

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
    -   在打擊點 (Hit stop) 插入 1-2 幀的 `Negative color (反白/負片)` 或 `Sketchy lines (粗糙線稿)`，強化打擊力度。
3.  **Frame Modulation (張數控制)**：
    -   **日常演技**：模擬 `Animation on 3s` (8fps)，保留手繪的頓挫感。
    -   **高潮戰鬥**：模擬 `Sakuga (作畫崩壞/高流暢)`，線條可瞬間變繁複或極簡，強調流暢度。