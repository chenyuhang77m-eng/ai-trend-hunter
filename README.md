# AI 热点捕手 · ai-trend-hunter

> 每日 10:00 自动归档全网 9 大平台热搜 / 热销榜单,按 8 大消费品类聚合,提供跨平台共振、双词云与营销 Playbook 的报刊式日更看板。

## 🌐 在线访问

部署在 GitHub Pages:**https://chenyuhang77m-eng.github.io/ai-trend-hunter/**

每天上午 10:00(北京时间)随数据源自动刷新,无需手动操作。

## 📦 数据来源

数据由 [`top-rank-tracker`](https://github.com/chenyuhang77m-eng/top-rank-tracker) 仓库的 GitHub Action 每天 10:00 自动抓取并归档,本页面通过 GitHub Raw 直接 `fetch` 最新 JSON,**无需后端**。

| 类别 | 平台 |
|---|---|
| 热搜榜(5) | 微博 / 百度 / 夸克 / 搜狗 / 360 |
| 电商榜(4) | 淘宝天猫 / 京东 / 快手电商 / 今日热卖 |

## 🧩 页面结构

| Section | 内容 |
|---|---|
| **01 热搜榜** | 5 大热搜平台 × TOP10 · 按 8 大品类筛选 |
| **02 热销榜** | 4 大电商平台 × TOP10 · 按 8 大品类筛选 |
| **03 趋势分析** | 各平台日热度走势 · 跨平台共振 TOP10 · 3日新晋/退榜商品(品牌/卖点维度) · 全网 TOP15 · 双词云(话题 vs 商品) · Editorial 编辑手记 |
| **04 营销建议** | 8 大品类 × 4-5 个二级品类 × 营销场景 × 话题钩子 × 投放策略,今日真实命中话题自动高亮 |

## 🏷️ 8 大品类体系

3C数码 · 家居家装 · 家用电器 · 母婴亲子 · 食品饮料 · 美妆护肤 · 服饰穿戴 · 平台教育

## 🎨 设计

- Editorial Newspaper 报刊版式(米黄纸张 + 墨黑 + 朱红 + 墨绿 + 金黄)
- 字体:Fraunces(意大利体显示)+ Noto Serif SC(中文衬线)+ JetBrains Mono(数据标签)
- 可视化:ECharts 5.4.3 + echarts-wordcloud 2.1.0
- SVG 噪点叠加增强纸张质感

## 🚀 本地预览

```bash
git clone https://github.com/chenyuhang77m-eng/ai-trend-hunter.git
cd ai-trend-hunter
# 直接双击 index.html,或起一个本地静态服务
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 📝 修改日志

### v1.0(2026-05-15)
- 初版上线:8 大品类 tab + 双词云 + 营销 Playbook + Editorial 手记
- 词典覆盖品牌词 ~300 / 卖点词 ~380 / 话题词 ~280
- 今日命中话题在营销建议表内高亮显示

## 📄 License

MIT
