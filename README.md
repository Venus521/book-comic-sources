# 墨记 · 统一源规则（书源 + 漫画源）

一份规则文件，端侧直连。平时电脑上筛好源、改这一个文件、push，手机 App 拉最新一份缓存到本地，端侧直连源站抓取，不经过任何云中转。

## 结构

- 顶层：`{ version, updated, count, sources: [...] }`
- `sources` 数组里每条带 `type` 字段：
  - `type: "book"` — 书源，Legado 形制（searchUrl + ruleSearch/ruleBookInfo/ruleToc/ruleContent）
  - `type: "comic"` — 漫画源，cmbok 形制（api engine / DOM config）
- 书源带 `probeTier`（A/B/C/E）门槛标注：A 免门槛直连可用，B 直连 200 但搜不出，C 需代理，E 需 JS 执行器（`usable: false`）。F 死源不收录。

## 维护方式

1. 电脑上探活筛选，改 `sources.json`（增源 / 删死源 / 替换 / 改门槛标注）；
2. 一个 commit，push 到 main；
3. 手机 App 启动或点「刷新源」从下面任一地址拉最新：

   - jsDelivr：`https://cdn.jsdelivr.net/gh/Venus521/book-comic-sources@main/sources.json`
   - GitHub raw：`https://raw.githubusercontent.com/Venus521/book-comic-sources/main/sources.json`

## 生成脚本

`D:/项目/书写笔记本/tools/build_sources_json.py`（从 venus-hub 的 curated/lightnovel/cmbok + 门槛标注生成，剔除 F 死源）。
