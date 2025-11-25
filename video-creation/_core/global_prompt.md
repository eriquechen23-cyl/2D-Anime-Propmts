# Global Master Prompt Template (GEMINI FLOW / 2D Anime)

## Master Prompt 結構指引
- **Duration**: 8s (短版) 或 15s (標準)
- **Style**: 必須包含 "2D Anime", "Cel Shading", "Manga Aesthetics"
- **Constraints**: 必須列出 "No Photorealism", "No 3D Gradients", "Flat Color"

```text
Master({Duration}s｜2D Anime / Cel Shaded｜9:16｜24fps｜{Style_Primary})
「{時間/地點}；{環境氛圍 (Toon Render)}。
主角：{角色名稱} ({User_Avatar_Description}，動漫化風格，帥氣男性)，穿著 {服裝}。
動作：{動作描述}。
畫面風格：日系 2D 動畫，{描邊粗細}px 輪廓線，高對比賽璐珞上色。
鏡頭語言：{運鏡方式}，保留 2D 平面構成感，視差控制在 2-6px。
漫畫特效：{高潮段落} 疊加網點 (Screen Tone) 與速度線，擬聲字 "{Sound_FX}" 出現。
光影設定：主光 {Color} 硬邊陰影 (Hard Shadow)，邊緣光 (Rim Light) {Color} 勾勒輪廓。
作畫技術 (Animation Tech)：
- 動態：{Smear Frames / Impact Frames / Limited Animation}
- 背景質感：{Hand-painted Watercolor / Poster Paint Style}
物理細節 (轉化為 2D)：
- 材質：{描述} (以色塊和高光形狀表現，非真實反射)
- 流體/粒子：{描述} (以 2D Sprite 或 Toon 渲染表現)
無字幕、無浮水印、無寫實質感。」