# DroneFlamesSiteMods

DroneFlames 官网社区 mod 目录仓。本仓只放一个数据文件 `site_catalog.json`，是 mod 上架**两段流**的第一段数据源，与游戏商店目录仓 [DroneFlamesModStore](https://github.com/xyu3032-commits/DroneFlamesModStore) 是两个独立的仓、两件独立的事。

官网门户页按 raw 直链拉取本文件展示社区库：

```
https://raw.githubusercontent.com/xyu3032-commits/DroneFlamesSiteMods/main/site_catalog.json
```

## 两段流操作法（站长）

### 第一段：上官网

作者的上架申请（issue）审核通过后，把作者 catalog 里对应的**条目**追加进 `site_catalog.json` 的 `mods` 数组，提交推送即生效（raw 有约 5 分钟 CDN 缓存）。

- 条目字段与商店 catalog 同构：`id` / `name` / `version` / `author` / `description` / `category` / `download_url` / `sha256` / `size` / `icon`。
- 可选字段：`source`（作者源 id，惯例为 `<mod id>_source`；不写时官网按官网目录自身处理）、`lang`（语言代码；不写时官网按下载文件名推断）。
- `download_url` 必须用 `raw.githubusercontent.com` 直链；`sha256` 与 `size` 必须与 .dfmod 实物一致（游戏下载后会双重校验，对不上拒装）。
- 此时条目在官网社区库带「官网首发 · 仅官网」徽标，**还不在游戏里**。

### 第二段：进游戏

官网展示期复核通过后，把作者的**源条目**加进 DroneFlamesModStore 仓根目录 `index.json` 的 `sources` 数组：

```json
{ "id": "<mod id>_source", "name": "<作者仓库名>", "url": "https://raw.githubusercontent.com/<作者>/<仓库>/main/mod_catalog/catalog.json" }
```

- 游戏商店（0.33.5.39+）随即能刷到该源的全部条目。
- 同一个 mod 在官网社区库会按 `id` + 下载文件名与商店目录自动对账：已进游戏的改显「已进游戏」徽标，不会重复出现两条。
- 下架：从本文件删条目 = 下官网；从 DroneFlamesModStore/index.json 删源 = 下游戏。两段独立，按需操作。

## English summary

This repo hosts `site_catalog.json`, the website-side community catalog for the DroneFlames mod portal (stage one of a two-stage listing flow). Adding an entry here lists the mod on the website's Community section only ("website first"); adding the author's source to `DroneFlamesModStore/index.json` afterwards is the separate stage two that puts the mod into the in-game store.
