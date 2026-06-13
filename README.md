<div align="center">

# 跨语言选购顾问 · Cross-Lingual Purchase Advisor

> *「你问 AI『最好的 X 是什么』，它把返佣榜单第一名读给你听。这个 skill 让它闭嘴，去查真东西。」*

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-cross--lingual--purchase--advisor-blueviolet)](skills/cross-lingual-purchase-advisor/SKILL.md)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-D97757?logo=anthropic&logoColor=white)](https://docs.claude.com/en/agents-and-tools/agent-skills/overview)
[![skills.sh](https://skills.sh/b/miles-byted/purchase-advisor-skill)](https://skills.sh/s/miles-byted/purchase-advisor-skill)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**把"被返佣榜单、厂商软文、刷量水帖污染的 AI 选购建议"，变成中英测评交叉验证、识破假洋品牌、确认国行质保的可执行结论。**

[看效果](#效果示例) · [安装](#快速开始) · [触发方式](#触发方式) · [它和同类有什么不同](#它和同类有什么不同) · [安全边界](#安全边界)

</div>

---

## 它解决什么问题

你想买台扫地机器人，问 AI「哪款最好」。它给你一份榜单——读起来像分析，其实下游是三股被污染的水：**返佣榜单**（为佣金排序）、**厂商软文**（伪装成测评的文案）、**刷量水帖**（批量种植的假口碑）。更糟的是，模型自己对大牌还带着可测的偏好。

普通做法（再问一次、换个词搜）治不了这个病，因为污染在信源层。这个 skill 换了个思路：**不信任何单一信源，用"独立性"和"跨语言交叉验证"筛真相**——英文独立测评站建基准线，中文横评做本地验证，两边求交集，再纠正 AI 自己的品牌先验，最后落到中国大陆买得到、保得了、算得清几年总成本的那一款。

## 效果示例

```text
你：帮我选一台 2000 元内的扫地机器人，要能扫拖一体、带自动集尘。

它（摘要）：
① 需求锁定 → 品类=本土强势，中文权重 70% / 英文 30%
② 英文线：RTINGS / Wirecutter Top 型号 + 各自"不推荐"项
③ 中文线：B站横评 / 知乎高赞实测 Top 型号 + 带货识别
④ 交叉验证表：🟢 双推 2 款 / 🟡 单推 3 款 / 🔴 矛盾 1 款
④½ 反事实去偏：剔除 1 款"只是有名"的大牌，国产平替顶上
⑤ 真实差评：某款集尘频繁堵塞（高频故障）
⑥-⑦ 假洋品牌排查 + 京东自营/国行质保确认
⑧ 年度总成本：机器 ÷ 5 年 + 耗材 + 电费 = ¥XXX/年
⑨ 推荐清单 / 不推荐清单 / 注意事项 / 交叉验证总结
```

## 快速开始

```bash
npx skills add miles-byted/purchase-advisor-skill
```

装完对 Agent 说：

```text
帮我选一台 2000 元内、扫拖一体的扫地机器人，要在中国大陆用
```

## 触发方式

- 「这个 X 怎么选 / 帮我选购」
- 「值得买吗 / 避坑 / 推荐一款」
- 「which X should I buy」
- 「A 和 B 哪个好，给我交叉验证」
- 「这是不是假洋品牌」
- 「国行有售吗 / 算下几年总成本」

## 它会交付什么

| 板块 | 交付物 |
|---|---|
| ✅ 推荐清单 | 排名 · 型号 · 理由 · 渠道 · 价格 · **年度总成本** |
| ❌ 不推荐清单 | 型号 · 原因 · 来源（含权威测评的 "Don't Buy"） |
| 📊 交叉验证总结 | 中英结果对比表 + 反事实去偏结论 |
| ⚠️ 注意事项 | 国行差异 / 假洋品牌 / 高频故障 |

## 它和同类有什么不同

| 维度 | 通用购物/比价 skill | [product-research](https://github.com/199-biotechnologies/product-research)（英文反营销） | [is-real-brand](https://github.com/zhongth/is-this-brand-fake.skill)（假洋牌专项） | **本 skill** |
|---|---|---|---|---|
| 信源 | 单边榜单 | 英文 owner-only 一手反馈 | 7 国工商/电商/社媒 | **中英双语交叉验证** |
| AI 自身偏见 | 不处理 | 反事实去偏 | 不处理 | **反事实去偏 ✅** |
| 假洋品牌 | 不识别 | 不识别 | **量化打分 + PDF 报告**（更深） | 四查快速过滤（流程内一步） |
| 大陆可购性 | 不管 | 不管 | 不涉及 | **国行/电压/质保确认 ✅** |
| 持有成本 | 只看售价 | 偶尔 | 不涉及 | **强制量化年度总成本 ✅** |
| 形态 | 工具/比价 | 单论点方法论 | 单论点专项工具 | **九步半选购流程** |

> **生态位关系（学手艺不偷皮）**：
> - 想做**深度品牌真伪调查 + PDF 报告** → 用 [is-real-brand](https://github.com/zhongth/is-this-brand-fake.skill)，它比我们的第六步深得多。
> - 想做**英文域反营销选品** → 用 [product-research](https://github.com/199-biotechnologies/product-research)。
> - 想要**给中国大陆买家、把"英文测评 + 中文实测 + 假洋牌排查 + 国行质保 + 持有成本"一次答完** → 本 skill。
> 反营销叙事与反事实去偏的思路致谢见文末。

## 安全边界

- **不下单、不支付、不点击购买链接**——只产出决策依据。
- **不编造**：找不到的信源/型号/数字写"未找到"，绝不为凑流程造假。
- 不替你判断"一定要买"——给推荐与不推荐两张清单，决定权在你。

## 文件结构

```
skills/cross-lingual-purchase-advisor/
├── SKILL.md                      # 九步半方法论主体
├── references/
│   └── trusted-reviewers.md      # 可信测评站名录 + 独立性/行货判断表
└── examples/
    └── robot-vacuum-walkthrough.md  # 真实选购实录（型号/测评立场均来自可点击信源，11 条 URL 实测可达）
```

## 验证与测试

验收 prompt：`帮我选一台 2000 元内、扫拖一体的扫地机器人`
合格表现：九步全有输出、含 ≥1 不推荐项、有反事实去偏结论、给出年度总成本数字、确认国行渠道。
想看输出长什么样？→ [一篇真实交叉验证实录](skills/cross-lingual-purchase-advisor/examples/robot-vacuum-walkthrough.md)（含中英信源对照、假洋品牌排查、年度成本估算）。

## 致谢

- 反营销 / 只信真买真用的一手反馈（owner-only）的信源思路 — [199-biotechnologies/product-research](https://github.com/199-biotechnologies/product-research)

## License

[MIT](LICENSE)

---

<div align="center">

*不信榜单，信交集。*

</div>
