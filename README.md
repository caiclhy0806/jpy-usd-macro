# JPY/USD Macro Driver Map

> 日元兑美元宏观驱动全景分析仪表盘（2010–2026）
> WorkBuddy 空间：`JPY-USD-Macro-Driver-Map`

## 概览
交互式单文件 HTML 仪表盘，分析日元兑美元的宏观驱动因子：
美联储 vs 日本央行利差、贸易差额、Brent 原油、美债 10Y 收益率、Carry Trade 逻辑、相关性热力图、因果链模型与动态驱动网络图。汇率以「每 100 日元兑美元」表示（数值越低=日元越弱）。

## 访问
- 🌐 线上站点（GitHub Pages）：https://caiclhy0806.github.io/jpy-usd-macro/
- 🔑 访问密钥：`cl2026`（打开页面输入后进入，同一浏览器会话内验证一次）
- 📦 仓库：`caiclhy0806/jpy-usd-macro`（公开）

## 版本链（可回退）
| 标签 | 说明 |
|------|------|
| `ver.001` | 原始未改动版本（基线） |
| `ver.002` | 新增访问密钥门禁 `cl2026` |
| `ver.003` | 顶栏版本徽章 + 更新记录小组件 |
| `ver.004` | 实时官方数据追踪模块（FRED 美国/日本 + World Bank 中国，逐卡标注来源）（当前线上） |

回退：`git checkout ver.001|ver.002|ver.003`，改完 `git push origin main`。

## 实时官方数据追踪（ver.004）
页面顶部新增「实时官方数据追踪」模块，按国家分组动态抓取并**逐卡标注来源**：
- **美国 / 日本**：经 FRED（圣路易斯联储）API 实时获取 —— 序列：DEXJPUS（USD/JPY）、FEDFUNDS（联邦基金利率）、DGS10（10Y 美债）、DCOILBRENTEU（Brent）、IRSTCB01JPM156N（日本政策利率）、JPNXTNTVA01CXMLM（日本贸易差额）。需在模块内填入免费 FRED API Key（https://fredaccount.stlouisfed.org/apikeys），Key 存于 sessionStorage，同一浏览器会话内免重复输入。
- **中国**：经 World Bank Open Data 实时获取（**无需 Key**）—— NY.GDP.MKTP.KD.ZG（GDP 增速，国家统计局）、TX.VAL.MRCH.CD.WT / TM.VAL.MRCH.CD.WT（货物出口/进口，海关总署）。
- 每张卡片显示最新值、数据日期与来源机构；并衍生「美日政策利差（Fed − BoJ）」。
- 历史走势图（①–⑩）仍为 2010–2026 官方年度均值的**静态基线**，本模块为在其之上追加的实时追踪层。

## 本机运行
```bash
cd /Users/cailei/WorkBuddy/JPY-USD-Macro-Driver-Map
python3 -m http.server 8000 --bind 127.0.0.1
# 浏览器打开 http://localhost:8000/ ，输入密钥 cl2026
```

## 更新流程（发新版）
1. 编辑 `index.html`
2. 在末尾 `VER_LOGS` 数组顶部加一条更新说明，并改标题的 `Ver x.x`
3. 提交并打标签：
   ```bash
   git add index.html
   git commit -m "ver.004 说明"
   git tag -a ver.004 -m "ver.004 说明"
   ```
4. 推送（用一次性内联令牌 URL，令牌取自 fx-tracker remote，勿写入 config）：
   ```bash
   git push "https://caiclhy0806:<TOKEN>@github.com/caiclhy0806/jpy-usd-macro.git" main --tags
   ```
5. GitHub Pages 随 `main` 自动重建（约 30–60 秒）。

## 备注
- 此空间为该项目的**唯一编辑/发版副本**（git 仓库，含完整历史与标签）。
- 另一份 `/Users/cailei/Desktop/AI/jpy-usd-macro/` 为从 GitHub 克隆的运行副本，当前正托管本地 http://localhost:8000/ 。
- 前端密钥仅为「防路人级」保护；敏感数据需改用服务端鉴权或私有仓库。
