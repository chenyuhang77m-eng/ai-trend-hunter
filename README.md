# AI 热点捕手

`AI 热点捕手` 是一个静态网页看板，用来展示每天的热搜榜、热销榜、趋势变化、双词云和内容策略洞察。

线上地址：

```text
https://chenyuhang77m-eng.github.io/ai-trend-hunter/
```

数据来自：

```text
https://github.com/chenyuhang77m-eng/top-rank-tracker
```

## 项目定位

这个仓库只负责前端页面展示，不负责抓取数据。

每日数据由 `top-rank-tracker` 自动生成并保存为 JSON，前端通过 GitHub Raw 直接读取这些静态文件。因此当前架构不需要后端服务，也不需要数据库。

网页本身不会每天生成一份 HTML 快照。每天留存的是数据源仓库里的日期数据，未来可以通过日期选择器读取历史数据回看当天页面。

## 页面结构

当前页面包含 4 个主要部分：

1. 热搜榜
   - 展示抖音、微博、百度、夸克、360 搜索等热搜榜
   - 支持按 8 个一级类目筛选

2. 热销榜
   - 展示淘宝天猫、京东、快手电商、今日热卖、京东图书等热销榜
   - 支持按 8 个一级类目筛选

3. 趋势分析
   - 平台热度走势
   - 跨平台共振
   - 新晋商品/品牌
   - 退榜商品/品牌
   - 全网热度 TOP
   - 热搜词云和热销词云

4. 内容策略
   - 按一级类目展示 3-5 个二级类目
   - 每个二级类目包含营销场景、热点词、话题词和内容策略
   - 内容策略不再输出固定投放尾句

## 8 个一级类目

页面目前使用以下 8 个一级类目：

- 3C 数码
- 家居家装
- 家用电器
- 母婴亲子
- 食品饮料
- 美妆护肤
- 服饰穿戴
- 平台/教育

其中 `平台/教育` 是合并展示类目，内部包含两类行业信号：

- 平台侧：外卖、本地生活、团购、滴滴/打车、酒旅、二手回收、电商平台等
- 教育侧：图书、童书、绘本、教材、教辅、考试备考、学习工具等

## 词云逻辑

词云数据优先读取：

```text
data/wordclouds/latest.json
```

词云分为四组：

- `topic`：全部热搜词云，只来自热搜榜
- `product`：全部热销词云，只来自热销榜
- `topicCategory`：按类目拆分的热搜词云
- `productCategory`：按类目拆分的热销词云

前端展示规则：

- 左侧“热搜话题词云”只读热搜词
- 右侧“电商商品/品牌词云”只读热销词
- 切换类目时，分别读取 `topicCategory` 或 `productCategory`
- 悬停词云词条时，会展示该词来自的榜单标题
- 如果词云文件不可用，前端会回退到浏览器内置规则切词

## 洞察逻辑

页面优先读取：

```text
data/insights/latest.json
```

洞察由数据源仓库中的 LLM 脚本生成，前端只负责展示。

当前规则：

- 每个一级类目生成 3-5 个二级类目
- 二级类目优先来自当天真实热搜信号
- 热销榜作为商品和卖点参考
- 如果 LLM 生成不足，使用固定二级类目池兜底
- 策略文案只保留内容策略，不展示固定投放建议

## 本地预览

如果只打开前端仓库，页面会读取线上数据源。

```bash
cd ai-trend-hunter
python -m http.server 8000
```

浏览器打开：

```text
http://localhost:8000
```

如果要同时预览本地数据源和本地前端，建议在两个仓库的共同上级目录启动静态服务，例如：

```bash
cd C:\Users\Admin\Desktop\codex-demo
npx http-server -p 4183 -a 127.0.0.1
```

然后打开：

```text
http://127.0.0.1:4183/ai-trend-hunter/index.html
```

本地预览时，前端会优先读取：

```text
http://127.0.0.1:4183/top-rank-tracker/data/latest.json
http://127.0.0.1:4183/top-rank-tracker/data/insights/latest.json
http://127.0.0.1:4183/top-rank-tracker/data/wordclouds/latest.json
```

## 技术结构

这是一个单文件静态页面：

```text
index.html
```

主要依赖：

- ECharts
- echarts-wordcloud
- GitHub Pages
- GitHub Raw JSON 数据

没有构建流程，没有 npm 前端依赖，也没有后端 API。

## 与数据源仓库的关系

前端仓库：

```text
ai-trend-hunter
```

负责：

- 页面布局
- 榜单筛选
- 图表渲染
- 词云渲染
- 洞察展示

数据源仓库：

```text
top-rank-tracker
```

负责：

- 每日抓取榜单
- 生成历史 JSON
- 生成 AI 洞察
- 生成词云
- 由 GitHub Actions 自动提交数据

## 注意事项

- GitHub Raw 数据可能有几分钟缓存
- GitHub Actions 定时任务可能延迟触发
- 本地预览如果看到旧数据，可以强制刷新浏览器
- 如果数据结构调整，前端和数据源仓库需要同步更新
