# relationship · 演员合作力导向图

一个基于 ECharts 的演员合作关系数据可视化项目，将演员与其合作作品以力导向图的形式呈现，支持搜索、筛选与高亮，适用于广播剧 / 配音 / 影视演员合作网络的探索与展示。

## 功能特性

- **力导向图布局**：自动计算节点位置，节点大小映射参演作品数量
- **合作关系可视化**：连线展示合作作品名称，双主角作品与配角合作以不同线宽 / 辉光区分
- **多部合作防重叠**：同一对演员合作多部作品时自动分配差异化曲率，避免曲线重叠
- **演员搜索**：输入姓名即可高亮该演员的合作网络，其余节点自动变暗
- **合作次数筛选**：一键高亮「合作 2 次」「合作 ≥3 次」的演员对及其作品边
- **悬停聚焦**：鼠标悬停节点时聚焦其合作关系（adjacency 高亮）
- **交互操作**：滚轮缩放、拖拽平移、节点可拖动
- **桌面 / 移动双端**：提供 `index.html`（桌面）与 `mobile.html`（移动端）两个版本

## 目录结构

```
relationship/
├── index.html       # 桌面端页面
├── mobile.html      # 移动端页面
├── data.json        # 演员与合作关系数据
└── README.md
```

## 数据格式

`data.json` 包含 `actors`（演员列表）和 `links`（合作关系）两个数组：

```json
{
  "actors": [
    { "name": "风镜" }
  ],
  "links": [
    {
      "source": "风镜",
      "target": "陶典",
      "workName": "今日离港",
      "sourceRole": "主役",
      "targetRole": "主役"
    }
  ]
}
```

| 字段 | 说明 |
| --- | --- |
| `actors[].name` | 演员姓名 |
| `links[].source` / `target` | 合作双方姓名（需与 actors 中的 name 一致） |
| `links[].workName` | 合作作品名称，显示在连线上 |
| `links[].sourceRole` / `targetRole` | 双方在该作品中的角色类型，`主役` 表示主角，其余视为配角 |

## 运行方式

由于页面通过 `fetch` 读取同目录的 `data.json`，**不能直接用 `file://` 打开**，需通过本地 Web 服务访问：

```bash
# 在项目根目录任选其一
python3 -m http.server 8000
#   → 浏览器访问 http://localhost:8000/index.html

# 或
npx serve
```

修改 `data.json` 后，点击页面左侧的「重载图表」按钮即可重新加载，无需刷新页面。

## 技术栈

- [ECharts 5.4.3](https://echarts.apache.org/) 图表渲染（CDN 引入）
- 原生 HTML / CSS / JavaScript，无构建依赖
- Google Fonts（Noto Serif SC / Noto Sans SC / JetBrains Mono）

## 截图

> 节点圆环大小 = 参演作品数；金色粗线为双主角合作，金色细线为含配角的合作；多次合作的连线会以青绿色高亮标注。
