# zhuda-engine-assets

豬大引擎（[zhuda-laya-engine](https://github.com/zhudaandzhuer/zhuda-laya-engine)）用的共用素材：2D 圖、給圖轉 3D 用的參考圖、可平鋪的材質。之後會陸續加入 3D 模型、音樂和音效。

給 AI agent 的取用說明在 [`AGENTS.md`](AGENTS.md)（英文）。重點只有一句：**先讀索引，再用網址抓單一檔案，不要把整個倉庫拉下來**（約 4 GB）。

```
https://raw.githubusercontent.com/zhudaandzhuer/zhuda-engine-assets/main/<索引裡的 path>
```

## 現在有什麼（2026-11-26）

1,715 件素材、2,880 個檔。每一類的數量和狀態在 [`catalog/kinds.json`](catalog/kinds.json)，每一類的總覽圖在 [`previews/`](previews)。

| 資料夾 | 內容 |
| --- | --- |
| `3d/props/` | 道具 299 件：單一物件、透明底、正面或側面，給圖轉 3D 用 |
| `3d/characters/` | 角色 68 個：A 字站姿的正面和背面各一張 |
| `3d/creatures/` | 生物 30 隻：側面和正面各一張 |
| `2d/style-targets/`、`2d/key-art/` | 七種畫風的標竿圖和主視覺 |
| `2d/ui/` | 介面元件和圖示表；切好的單一圖示在 `2d/ui/icons/` |
| `2d/characters/` | 2D 角色、敵人、表情表（切好的單張在 `faces/<角色>/`） |
| `2d/scenes/`、`2d/backgrounds/`、`2d/backdrops/` | 橫向捲軸場景分層、俯視地磚、視覺小說背景、直式背景、遠景橫條 |
| `2d/symbols/`、`2d/cards/`、`2d/effects/` | 老虎機符號、卡牌、特效 |
| `textures/materials/<名稱>/` | 材質 173 種：`albedo`、`height`，做過後製的還有 `normal` 和 512 版 |
| `textures/` 其他 | 遮罩、貼花、飾邊條、植物片、角色零件（虹膜、皮膚、衣料印花）、細節圖、天空 |

畫風：古風寫實（`ancient`）、末日寫實（`ruin`）、卡通（`toon`）、手繪（`painted`）、科幻（`scifi`）、西方奇幻（`fantasy`）、現代都市（`city`）。

## 每件素材的狀態

索引裡每一筆都有 `status`：

| 狀態 | 意思 |
| --- | --- |
| `ok` | 規格用程式量過、縮圖看過，符合當初的要求。**沒有人逐張放大看過** |
| `flagged` | 可以用，但有 `issues` 寫的那個問題（例如被畫面邊緣切到、視角略斜） |
| `raw` | 生成後還欠一步後製（還沒接成無縫、還沒拼成完整天空），`issues` 會寫是哪一步 |
| `redo` | 畫錯了，不要用。留著是為了重做時對照 |

## 這些圖是怎麼來的

全部是 AI 生成的（gpt-image-2.6，另有一張是 Qwen-Image 2.1），2026 年 11 月分兩批做，加上先前做好的 48 種材質。第二批每張的提示詞在 `catalog.json` 的 `prompt`。提示詞都要求不要有文字、商標、真人和特定作品的角色；放大抽看過幾張沒有發現，但沒有逐張確認。唯一不是 gpt-image 做的是一把長柄兵器（`3d/props/ancient-crescent-blade-halberd`）。

已知的問題都寫在各筆的 `issues` 裡，比較大的幾類：

- 第二批有 12 張生物被畫成四足獸（哥布林、巨魔、史萊姆、幽魂、樹人、石魔像），標成 `redo`。
- 視覺小說背景有 16 張不管什麼場所都是霓虹雨夜的色調，標成 `flagged`。
- 第二批的 50 種材質還沒做成無縫、沒有法線；8 張天空還沒拼接。標成 `raw`。
- 道具都還只是參考圖，沒有任何一件轉成 3D 模型。

## 授權

**還沒決定。** 在這裡寫明之前，這些素材保留所有權利；公開放在這裡是為了讓作者自己的工具取用。

別人做的素材（Kenney、Poly Haven 這類有各自授權的素材包）不在這裡，在 [agentDevelopResources](https://github.com/zhudaandzhuer/agentDevelopResources)。
