# 每日股市监控静态看板

本目录是零依赖网页看板版本。当前版本已按原 PDF 报告章节扩展，并新增 `日更数据表格` 区，不只是总览看板。

页面顶部是模块导航，点击后跳转到对应模块；所有模块按页面顺序展开显示。PDF 标注口径不再单独成表，而是作为相关日更表格下方的动态标注显示。

## 打开方式

可以直接双击 `index.html` 打开。页面会优先读取 `data/current.js`，因此不依赖浏览器允许 `file://` 下的 JSON 请求。

也可以用本地 HTTP 服务打开：

```bash
python3 -m http.server 8765
```

打开：

```text
http://127.0.0.1:8765/
```

如果要让同一局域网里的其他设备访问，需要绑定到本机网卡：

```bash
python3 -m http.server 8765 --bind 0.0.0.0
```

然后在其他设备上访问 `http://你的Mac局域网IP:8765/`。`127.0.0.1` 只代表当前设备自己，不能给另一台设备用。

## 更新数据

把模型生成的标准 JSON 覆盖到：

```text
data/current.json
```

同时重新生成 `data/current.js` 和 `data/daily_tables.js`，刷新浏览器即可看到新数据。

```bash
python3 build_daily_tables.py
```

## 数据来源

当前样例数据来自 `outputs/market_daily_model/daily_from_csv_2026-07-27.json`。

PDF 表格来自 `/Users/yangtianyu/Downloads/每日股市监控报告 - 2026年7月27日.pdf`，仅作为表格结构模板与覆盖审计，不作为看板的日更数据源。日更看板表格来自：

```text
data/current.json
data/current.js
data/daily_tables.json
data/daily_tables.js
```

## 覆盖模块

- 总览与仓位
- 报告章节覆盖矩阵
- 日更数据表格区（36 张表 / 215 行，由 current.json 自动生成；1-13 章标注随数据日期动态更新）
- 全球多市场交叉验证
- A股大盘画像
- 六大板块聚类
- 核心个股池
- 情绪周期与市场风格
- 资金与龙虎榜
- 三类观测指标
- 波动率与升贴水实操
- 非对称性与多空比价
- 每日盘前 10 点检查
- 交易系统框架

## 审计

覆盖审计见：

```text
pdf_coverage_audit.md
```

当前审计结论：PDF 主章节与关键子模块均已有对应看板入口；仍需 FundDB/行情源强化全量动态数据。
