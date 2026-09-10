# 与 facet 的边界

talk-skills 和 [facet](https://github.com/webkubor/facet) 是同一条链的两段，**互不越界**：

| | talk-skills | facet |
|---|---|---|
| 管什么 | **说什么、怎么组织、什么语气** | **长什么样** |
| 具体 | 结论先行 / SCQA / MECE / 分组归属 / 读者定位 / 语气姿态 / 讲稿站位 | 字阶、密度、留白、分页、配色、模板、PDF 与长图渲染 |
| 产物 | Markdown 内容 | PDF / 长图 / 可分享站点 |
| 何时用 | 动笔前到定稿前 | 定稿后 |

**协作方式**：用 talk-skills 把内容写对，交给 facet 渲染。

```bash
# 内容定稿后
npx facet --input talk.md --template wechat-magazine --output talk.pdf
```

**不要在 talk-skills 里写排版规范**（字号、留白、分页阈值），那些是 facet 的 `docs/design-spec.md` 管的，重复写必然漂移。反过来，facet 不管内容的逻辑结构和语气——那是本仓的事。

**边界上的一条**：演讲版和阅读版是同一份内容的两个刻面（facet 的站点就这么做的：阅读版连续长文、演讲版一屏一章节）。**刻面切换是 facet 的能力，但两种刻面下内容该怎么组织是 talk-skills 的事**——演讲版要一屏一个论点、阅读版可以层层递进。
