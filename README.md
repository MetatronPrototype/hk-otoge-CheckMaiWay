# 香港音游CheckMaiWay

香港音游CheckMaiWay 是一个香港街机音游地图与跨境出行检查工具，覆盖 maimaiDX、CHUNITHM、beatmania IIDX、SOUND VOLTEX。它把公开机厅资料、地图链接、营业时间、机种信息、起点到机厅的参考交通路线，以及返程口岸/港铁时间约束放在同一个静态网页里，方便手机和电脑随时查看。

它不是实时排队系统，也不是官方导航。页面中的机台数量、营业时间、票价、路线、口岸安排和人气值均为公开资料整理后的参考信息，出发前仍应以机厅现场、官方交通/口岸信息和地图软件为准。

当前版本：`v1.2.2`

当前工程状态：

- `outputs/site` 当前提交：以 `main` 最新提交为准
- 数据生成日期：`2026-10-22`
- 当前统计：21 间机厅、8 个起点
- 当前机种覆盖：maimaiDX 20 间、CHUNITHM 13 间、beatmania IIDX 4 间、SOUND VOLTEX 4 间

## 公开地址

- Cloudflare Pages: <https://hk-otoge-checkmaiway.pages.dev/>
- GitHub Pages: <https://metatronprototype.github.io/hk-otoge-CheckMaiWay/>

未确认存在其他公开生产域名。

## 功能概览

### 地图与机厅列表

- 香港机厅地图总览，支持桌面和移动端。
- 欢迎页展示统计、数据来源、免责声明和版本号，进入地图后再显示完整信息。
- 地图缩放或移动时，列表同步显示当前地图范围内的机厅。
- 点击地图上的机厅标记后，侧边栏或移动端下方列表会自动滚动到对应店铺卡片。
- 选中机厅时，地图显示定位标记，列表卡片显示呼吸高亮。
- 支持按店名、地址、地区、机种搜索。
- 支持机种筛选，初始显示全部；单点一个机种进入单机种显示，再点其他机种进入多选。
- 支持本地收藏，收藏数据保存在用户自己的浏览器。
- 支持亮色模式和 OLED 纯黑暗黑模式；地图瓦片保持亮色以保证可读性。

### 店铺信息

每张店铺卡片展示：

- 店名、地区、地址
- 营业时间色块
- maimaiDX / CHUNITHM / IIDX / SDVX 机台信息
- 人气值
- 最近港铁站
- 数据来源与更新时间
- Apple 地图、Google 地图、BEMANI CN、Zenius-I-vanisher 链接

Google 地图链接使用店名 + 地区 + 地址 + 香港生成搜索查询，避免纯坐标链接只能落到地图点而不能匹配具体店铺。Apple 地图链接保留店名、地址和经纬度组合。

### 出行路线与推荐

当前支持 8 个起点：

- 西九龙高铁站 / 高铁西九龙口岸
- 罗湖口岸
- 落马洲支线 / 福田口岸
- 皇岗口岸（新口岸）
- 深圳湾口岸
- 香园围 / 莲塘口岸
- 港珠澳大桥香港口岸
- 香港国际机场 / 机场快线机场站

路线模块会：

- 按起点和目标机厅估算去程交通费和理论最快路线时间。
- 比较港铁/接驳方案与直接步行方案；如果步行更快，显示步行路线而不是强制绕港铁。
- 使用 `WALK_ROUTE_FACTOR=1.25` 对坐标距离进行步行时间折算，避免直线距离过度乐观。
- 显示相关港铁线路色块、小徽标和地图线路叠加。
- 在包含接驳巴士的路线中显示独立 BUS 色块、编号和参考票价。
- 显示最终步行段和步行时间。
- 根据当前起点置顶“最近机厅”和“路费最低”推荐，并用绿色呼吸环标记。

当前内嵌接驳模型覆盖有限场景，例如 B2P、B7、B5。它不是全香港公交/渡轮最优路线搜索。

### 返程红线

返程模块会分开显示：

- 最终离店红线
- 口岸过关红线
- 港铁/机场快线末班红线

计算原则：

- 口岸红线预留至少 30 分钟过关缓冲。
- 港铁末班红线预留入闸缓冲。
- 如果口岸关闭红线早于港铁末班红线，最终红线以口岸关闭倒推为准。
- 香港国际机场不套用口岸关闭时间，只显示机场快线/港铁相关约束和班次提示。
- 机场起点单独显示普通游客价格、套用优惠后价格和优惠条件。

## 数据来源与口径

主要来源：

- BEMANI CN
- Zenius-I-vanisher
- MTR 官方 HRRoutes API
- MTR 机场快线时间表
- 香港入境事务处口岸办公时间
- 公开巴士票价参考资料
- 公开社群和店铺备注

当前数据生成于 `2026-10-22`。机厅、机台、营业时间、路线和价格都有时效性，需要周期刷新。

皇岗口岸数据按运输署及入境处公开资料更新：皇岗口岸 24 小时运作，港方口岸区设有公共运输交汇处；本页路线模型暂以 B10 至青衣站接驳港铁作为代表方案，实际仍可选择 B11、B12、B13、B14、B15、NB73、专线小巴或跨境巴士。

人气值是固定的公开社群热度指标，来源于 BEMANI CN 收藏数、目标机台数量、更新时间和双来源核验等信号加权。它不代表实时排队人数、实时客流或现场拥挤程度。

## 免责声明

本页面仅供出行和选店参考。机台数量、版本、营业时间、店铺状态、票价、价格、路线、口岸安排与现场人流可能随时变化。所有价格仅供参考。出发前请以机厅现场、官方交通、官方口岸信息和主流地图软件为准。

路线时间为地图理论最快路线估算，未包含实时等车、拥堵、临时服务调整、站内复杂换乘和完整步行导航。接驳巴士模型仅覆盖当前站点内嵌的有限路线。

## 本地运行

这个站点是静态单页应用，不需要构建步骤。

在站点仓库目录运行：

```bash
python3 -m http.server 4173
```

然后打开：

```text
http://127.0.0.1:4173/
```

也可以直接打开 `index.html`，但建议用本地 HTTP 服务验证地图、图标、manifest 和浏览器存储行为。

## 静态部署

站点入口是：

```text
index.html
```

当前已验证的公开部署为：

- Cloudflare Pages
- GitHub Pages

由于这是静态站点，也可部署到其他静态托管平台，但 README 只声明当前已确认的公开地址。

## 工程结构

公开站点仓库位于 `outputs/site`，主要文件：

- `index.html`：完整单页应用，内嵌站点数据、样式和脚本。
- `README.md`：对外发布 README，也给维护者和 AI 读取工程背景。
- `assets/`：站点图标等静态资源。
- `site.webmanifest`：PWA/图标相关 manifest。
- `.nojekyll`：GitHub Pages 静态发布兼容文件。

完整维护工作区还包含：

- `outputs/hk_arcade_map.html`：独立 HTML 副本。
- `work/`：数据抓取、刷新、合并和复核工具及缓存。
- 根目录 `LAST_UPDATED.md`：本地完整工作区的重大更新记录。
- 根目录 `LAST_WORKING.md`：本地完整工作区的设计原则、约束和维护方向。

注意：`LAST_UPDATED.md` 和 `LAST_WORKING.md` 位于 `outputs/site` 这个内层 Git 仓库之外，不应在公开 README 中写成 GitHub 相对链接。

## 数据刷新与验证流程

数据刷新应在完整维护工作区执行，而不是只在 `outputs/site` 内执行。

可复核的现有工具包括：

- `work/fetch_bcn_current.mjs`：整理 BEMANI CN 当前店铺资料。
- `work/update_arcade_data.mjs`：合并 BEMANI CN、ZIv 和人工补充数据，并写回站点内嵌 JSON。
- `work/refresh_mtr_fares.mjs`：通过 MTR HRRoutes API 刷新起点到目标港铁站的票价、时间和路径。
- `work/refresh_mtr_last_trains.mjs`：通过 MTR HRRoutes API 的 `lastTrain` 字段刷新返程末班车资料。
- `work/add_airport_origin.mjs`：写入香港国际机场起点、机场快线票价、优惠条件、线路和返程末班信息。
- `work/embed_route_station_details.mjs`：从 MTR 重铁资料嵌入站点所需站点坐标和线路信息。

当前工作区没有可复核的 `work/build_surface_routes.mjs`，不要把它写入刷新命令或自动化流程。

建议刷新流程：

1. 刷新或复核 BEMANI CN 与 ZIv 数据。
2. 更新机厅数据，确认 21 间机厅和四机种口径是否变化。
3. 刷新 MTR 票价、路线、站点坐标和返程末班车信息。
4. 复核口岸办公时间、机场快线条件和接驳巴士参考票价。
5. 检查页面中的数据生成日期、免责声明和价格更新时间。
6. 用本地 HTTP 服务验证桌面和移动端：
   - 欢迎页统计和版本号。
   - 地图/列表联动。
   - 点击地图标记后列表滚到对应卡片。
   - 搜索、筛选、收藏。
   - 起点/终点路线、推荐、票价、返程红线。
7. 正式更新时同步版本号和项目记录。

## 版本与项目记录

正式更新必须带明确版本号，并同步检查：

- `outputs/site/README.md` 的当前版本。
- `outputs/site/index.html` 的 `APP_VERSION`。
- 根目录 `LAST_UPDATED.md`。
- 根目录 `LAST_WORKING.md`。

`LAST_UPDATED.md` 记录已经完成并验证的重大功能、修复、架构变化和被替代路线。`LAST_WORKING.md` 记录当前设计思路、取舍、约束和仍在推进的方向。如果某次更新没有新的可确认设计思路，`LAST_WORKING.md` 可以不增加正文，但必须确认现有内容没有过时。

## 已替代的设计路线

当前 README 只说明现状，完整历史请看本地完整工作区的 `LAST_UPDATED.md`。

已替代路线包括：

- 不再首次打开就直接进入信息密集地图，已改为欢迎页后进入地图。
- 不再默认使用暗色地图瓦片，暗黑模式下仍保留亮色地图以提高可读性。
- 不再使用纯坐标 Google 地图链接，改用店名 + 地区 + 地址 + 香港匹配具体店铺。
- 不再强制所有路线走港铁，改为比较港铁/接驳与步行候选。
- 不再裸写“最便宜”，改用“路费最低”等交通语义。

---

# Hong Kong Otoge CheckMaiWay

Hong Kong Otoge CheckMaiWay is a public arcade rhythm game map and cross-border trip checking tool for Hong Kong. It covers maimaiDX, CHUNITHM, beatmania IIDX, and SOUND VOLTEX, combining arcade locations, game availability, opening hours, map links, route estimates, fare references, and return-trip deadline checks in one static web page.

It is not a real-time queue system and it is not an official navigation product. Machine counts, opening hours, fares, routes, checkpoint arrangements, and popularity scores are reference data only. Always verify with the arcade, official transport/checkpoint information, and map apps before travelling.

Current version: `v1.2.2`

Current project state:

- `outputs/site` current commit: latest `main`
- Data generated on: `2026-10-22`
- Current dataset: 21 arcades and 8 origins
- Current game coverage: 20 maimaiDX arcades, 13 CHUNITHM arcades, 4 IIDX arcades, 4 SOUND VOLTEX arcades

## Live Sites

- Cloudflare Pages: <https://hk-otoge-checkmaiway.pages.dev/>
- GitHub Pages: <https://metatronprototype.github.io/hk-otoge-CheckMaiWay/>

No other production domain is confirmed in the current project records.

## Features

### Map and Arcade List

- Hong Kong arcade map optimized for desktop and mobile use.
- Welcome screen with totals, data sources, disclaimer, and version number.
- The arcade list follows the current map viewport when the map is moved or zoomed.
- Clicking an arcade marker scrolls the side or lower list to the matching arcade card.
- Selected arcades are highlighted both on the map and in the list.
- Search by arcade name, address, district, and game category.
- Game filters show all games by default; selecting one category switches to that category, and selecting more categories enables multi-select filtering.
- Browser-local favorites, stored only in the user's browser.
- Light mode and OLED black dark mode. Map tiles stay bright for readability.

### Arcade Cards

Each arcade card shows:

- Arcade name, district, and address
- Opening-hour badge
- maimaiDX / CHUNITHM / IIDX / SDVX availability
- Popularity score
- Nearest MTR station
- Source and update metadata
- Apple Maps, Google Maps, BEMANI CN, and Zenius-I-vanisher links

Google Maps links are generated from arcade name + district + address + Hong Kong instead of coordinates only, so the map app has a better chance of matching the actual shop POI. Apple Maps links keep the name, address, and coordinates.

### Routes, Recommendations, and Fare References

Supported origins:

- Hong Kong West Kowloon Station / West Kowloon Control Point
- Lo Wu Control Point
- Lok Ma Chau Spur Line / Futian Control Point
- Huanggang Port (new co-location port)
- Shenzhen Bay Control Point
- Heung Yuen Wai / Liantang Control Point
- Hong Kong-Zhuhai-Macao Bridge Hong Kong Port
- Hong Kong International Airport / Airport Express Airport Station

The route module:

- Estimates outbound transport fare and theoretical fastest route time for the selected origin and arcade.
- Compares MTR/feeder candidates against direct walking and shows walking when it is faster.
- Uses `WALK_ROUTE_FACTOR=1.25` to convert coordinate distance into a less optimistic walking-time estimate.
- Shows MTR line badges, line reference colors, small route logos, and map route overlays.
- Shows feeder bus badges, route numbers, and reference fares where the current model includes a feeder.
- Shows the final walking segment and walking time.
- Pins the nearest arcade and the lowest-route-fare arcade for the selected origin with a green pulse highlight.

The feeder model is limited. It currently covers embedded cases such as B2P, B7, and B5. It is not a full Hong Kong bus/ferry route planner.

### Return Deadlines

Return-trip cards separate:

- Final departure deadline
- Border checkpoint clearance deadline
- MTR / Airport Express last-train deadline

Rules:

- Border checkpoint deadlines include at least a 30-minute clearance buffer.
- MTR last-train deadlines include an entry buffer.
- If the checkpoint closing constraint is earlier than the MTR last-train constraint, the final deadline follows the checkpoint constraint.
- Hong Kong International Airport is not treated as a border checkpoint, so it does not use checkpoint closing hours.
- Airport-origin routes show regular visitor fare, discounted fare, and the discount conditions separately.

## Data Sources and Scope

Main sources:

- BEMANI CN
- Zenius-I-vanisher
- MTR official HRRoutes API
- MTR Airport Express timetable
- Hong Kong Immigration Department checkpoint opening hours
- Public bus fare references
- Public community and arcade notes

The current data was generated on `2026-10-22`. Arcades, machine counts, opening hours, transport fares, and routes can become stale and should be refreshed periodically.

Huanggang Port is updated from public Transport Department and Immigration Department information: the port operates 24 hours and the Hong Kong Port Area has a public transport interchange. The current route model uses B10 to Tsing Yi Station as the representative rail connection; travellers may also use B11, B12, B13, B14, B15, NB73, green minibus routes, or cross-boundary coaches.

Popularity is a fixed public-community heat score. It is derived from signals such as BEMANI CN favorites, target machine counts, update recency, and cross-source verification. It does not represent live queue length, real-time crowding, or current foot traffic.

## Disclaimer

This page is for trip planning and arcade selection reference only. Machine counts, versions, opening hours, arcade status, fares, route times, checkpoint arrangements, and crowd levels may change at any time. All prices are reference values only. Verify with the arcade, official transport sources, official checkpoint information, and mainstream map apps before departure.

Route times are theoretical fastest-route estimates. They do not include real-time waiting, traffic, temporary service changes, complex in-station transfer time, or full walking navigation. The feeder bus model only covers the limited routes embedded in the current site.

## Local Run

This is a static single-page app and has no build step.

From the site repository directory:

```bash
python3 -m http.server 4173
```

Then open:

```text
http://127.0.0.1:4173/
```

Opening `index.html` directly may work, but a local HTTP server is preferred when checking map assets, icons, manifest behavior, and browser storage.

## Static Deployment

The site entry point is:

```text
index.html
```

Confirmed public deployments:

- Cloudflare Pages
- GitHub Pages

The app can technically be hosted on other static providers, but this README only lists confirmed public deployments.

## Project Structure

The public site repository is `outputs/site`:

- `index.html`: complete single-page app with embedded data, styles, and scripts.
- `README.md`: public README for visitors, maintainers, and AI code readers.
- `assets/`: icons and static assets.
- `site.webmanifest`: web app manifest.
- `.nojekyll`: GitHub Pages compatibility marker.

The complete maintenance workspace also contains:

- `outputs/hk_arcade_map.html`: standalone HTML copy.
- `work/`: data refresh, merge, verification tools, and source caches.
- Root `LAST_UPDATED.md`: local major-update record for the full workspace.
- Root `LAST_WORKING.md`: local design principles, constraints, and maintenance direction for the full workspace.

Note: `LAST_UPDATED.md` and `LAST_WORKING.md` live outside the inner `outputs/site` Git repository. They should not be linked as GitHub-relative README links from this public site repository.

## Data Refresh and Verification

Run data refreshes from the complete maintenance workspace, not from `outputs/site` alone.

Available tools in the current workspace:

- `work/fetch_bcn_current.mjs`: prepares current BEMANI CN shop data.
- `work/update_arcade_data.mjs`: merges BEMANI CN, ZIv, and curated local data into the embedded site JSON.
- `work/refresh_mtr_fares.mjs`: refreshes MTR fare, time, and path data from HRRoutes.
- `work/refresh_mtr_last_trains.mjs`: refreshes return last-train data from the HRRoutes `lastTrain` field.
- `work/add_airport_origin.mjs`: adds the Hong Kong International Airport origin, Airport Express fares, discount conditions, route lines, and last-train data.
- `work/embed_route_station_details.mjs`: embeds MTR station coordinates and line information needed by the route map.

The current workspace does not contain a verifiable `work/build_surface_routes.mjs`; do not document or run it as part of the active refresh flow.

Suggested refresh flow:

1. Refresh or verify BEMANI CN and ZIv source data.
2. Update arcade data and check whether the 21-arcade, four-game scope has changed.
3. Refresh MTR fares, route paths, station coordinates, and return last-train data.
4. Recheck checkpoint hours, Airport Express conditions, and feeder bus reference fares.
5. Check the data generation date, disclaimer text, and fare update labels in the page.
6. Run a local HTTP server and verify desktop/mobile behavior:
   - Welcome totals and version.
   - Map/list synchronization.
   - Marker click scrolls to the matching arcade card.
   - Search, filters, and favorites.
   - Origin/destination route, recommendations, fare display, and return deadlines.
7. Update the version and project records for any formal release.

## Version and Project Records

Every formal update must have an explicit version number and must check:

- Current version in `outputs/site/README.md`.
- `APP_VERSION` in `outputs/site/index.html`.
- Root `LAST_UPDATED.md`.
- Root `LAST_WORKING.md`.

`LAST_UPDATED.md` records completed and verified major features, fixes, architecture changes, and replaced directions. `LAST_WORKING.md` records current design thinking, tradeoffs, constraints, and ongoing direction. If an update adds no new confirmed design direction, `LAST_WORKING.md` may stay unchanged, but its existing content must still be checked for staleness.

## Replaced Directions

This README describes the current state. Full history belongs in the full workspace's `LAST_UPDATED.md`.

Replaced directions include:

- The app no longer opens directly into the dense map view; it now starts with a welcome screen.
- Dark map tiles are no longer the dark-mode default; bright map tiles are kept for readability.
- Google Maps links are no longer coordinate-only; they use arcade name, district, address, and Hong Kong.
- Routes no longer force MTR for every origin/destination pair; the model compares MTR/feeder and walking candidates.
- The bare label "cheapest" was replaced with route-fare language such as lowest route fare.
