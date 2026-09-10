<h1 align="center">talk-skills</h1>

<p align="center">
  把话说对的四步：搭骨架 → 定读者 → 调语气 → 当读者读一遍。<br/>
  给 AI agent 和人共用的表达规范。
</p>

<p align="center">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-0f766e.svg" /></a>
  <img alt="Skills" src="https://img.shields.io/badge/skills-4-111827.svg" />
  <img alt="Claude Code" src="https://img.shields.io/badge/Claude%20Code-ready-d97706.svg" />
  <img alt="Codex" src="https://img.shields.io/badge/Codex-ready-111827.svg?logo=openai&logoColor=white" />
  <img alt="Cursor" src="https://img.shields.io/badge/Cursor-ready-000000.svg" />
</p>

---

写文档、提单、写评审意见、准备分享——**内容对了但没人看完，或者看完了对方先想辩解**，通常不是内容问题，是这四件事没按顺序做：

```
① 搭骨架   结论先行 · SCQA 四句 · MECE 不重不漏
② 定读者   给人 or 给 agent；对上 or 对同侧
③ 调语气   归因情境 · 自曝先行 · 认对方贡献 · 允许被推翻
④ 当读者   以第一次看的人的身份通读，带清单查错
```

跳过 ④ 的实测代价：一份 9918 字的技术报告，通读后揪出 20 处问题，**19 处是通读才发现的**——内容错位挂到邻节、引用已删章节、同一份文档两处结论互相打脸。脚本只能扫出词面残留。

## 四个 skill

| skill | 管什么 | 什么时候用 |
|---|---|---|
| **how-to-write** | 总纲：上面四步的完整方法 | 写任何要给别人看的文字之前 |
| **peer-facing-writing** | 对同事的书面沟通：提单骨架、逐句替换表 | 写 issue、评审意见、跨团队报告 |
| **talk-text-review** | 讲稿姿态：这份稿是「我教你们」还是「我跟你们聊」 | 对同级或高手分享之前 |
| **talk-visual-review** | 讲稿视觉验收 | 出片之前 |

## 装上就能用

```bash
git clone git@github.com:webkubor/talk-skills.git
cp -r talk-skills/skills/* ~/.claude/skills/     # Claude Code
```

其他 agent 的装法、以及规范背后的依据见 [AGENTS.md](AGENTS.md)。

## 它不管什么

表达拆成四段，本仓只管第一段，其余各有归属，互不重复定义：

| 说什么 | 长什么样 | 怎么念 | 在哪写 |
|---|---|---|---|
| **talk-skills** | [facet](https://github.com/webkubor/facet) | [voxflow](https://github.com/webkubor/voxflow) | [typora-Bloom-theme](https://github.com/webkubor/typora-Bloom-theme) |
| 结构 · 语气 · 归属 | 字阶 · 留白 · 分页 · 渲染 | 声音设计 · 戏感 · 停顿 | 编辑器环境 |

一句话判归属：「该说什么、先说哪句、这话得罪人吗」→ 本仓；「字号多大、留多少白」→ facet；「这句怎么念」→ voxflow。完整分工见 [BOUNDARY.md](BOUNDARY.md)。

## 为什么规则长这样

语气部分的每条规则都挂着一个心理学机制，不是「礼貌一点」这种手感：

- **基本归因错误** → 别写「测试方法不对」，写「这个坑在页面上看不出来」（归因到情境，不归因到人）
- **面子威胁** → 命令式触发防御，对方先保护自尊、后处理信息
- **逆火效应** → 直接说「你错了」会让人更坚持，尤其在有第三方围观的单据里
- **自曝降防御** → 同一个坑自己也踩过，先写自己踩过

结构部分用金字塔原理（Barbara Minto）：结论先行、以上统下、归类分组（MECE）、逻辑递进。

MIT License.
