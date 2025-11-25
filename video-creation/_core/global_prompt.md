# Global Master Prompt Template (GEMINI FLOW / 2D Anime)

## Master Prompt 結構指引
- **Duration**: 8s (短版) 或 15s (標準)
- **Style**: 必須包含 "2D Anime", "Cel Shading", "Manga Aesthetics"
- **Constraints**: 必須列出 "No Photorealism", "No 3D Gradients", "Flat Color"

```text
Master({Duration}s｜Jujutsu Kaisen Style / MAPPA Aesthetics｜16:9｜24fps｜Dark Fantasy Action)
「{時間/地點}；{環境氛圍 (Toon Render)}。
主角：{角色名稱} ({User_Avatar_Description}，動漫化風格，帥氣男性)，穿著 {服裝}。
動作 (Act & Beat)：{動作描述，請依照 Act 1 (Setup) -> Act 2 (Conflict) -> Act 3 (Climax) 結構撰寫，並標記 Beat}。
畫面風格：MAPPA Animation Style，Rough Sketchy Lines (粗獷線條)，High Contrast Cel Shading (高反差賽璐珞)。
空間佈局 (Spatial Layout)：
- 多層景深 (Deep Depth of Field)：區分 [Foreground: 模糊前景/特效] -> [Midground: 交戰] -> [Background: 透視延伸]。
- 體積感 (Volume)：角色與怪物具備 3D 體積感 (Three-quarter view/Extreme Angle)，避免平面貼圖感。
鏡頭語言 (Angle & Continuity)：{運鏡序列描述，包含 Sequence Logic 與 Match Cut}，強調 Z 軸縱深與透視變形 (Foreshortening)...
漫畫特效：{高潮段落} 疊加網點 (Screen Tone) 與放射狀速度線 (Converging Speed Lines)，擬聲字 "{Sound_FX}" 出現。
光影設定：Moody Low-key Lighting (低調光)，Deep Blue/Purple Shadows (冷色陰影)，Volumetric Lighting (體積光)。
作畫技術 (Animation Tech)：
- 動態：{Smear Frames / Black Flash Effect (Negative Color) / Hyper-dynamic Camera}
- 背景質感：{Hand-painted Watercolor / Poster Paint Style}
物理細節 (轉化為 2D)：
- 材質：{描述} (以色塊和高光形狀表現，非真實反射)
- 流體/粒子：{Cursed Energy Fluid / Ink Brush Texture / Floating Dust Particles}
無字幕、無浮水印、無寫實質感。」
```