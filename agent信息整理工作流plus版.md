---
tags: [工作流, agent, 知识管理, Deep Research]
created: 2026-07-18
status: v1-plus
---

# Agent 信息整理工作流（Plus 版 / Deep Research 模式）

> 完整版工作流。当需要**高质量、多源验证、学术级严谨**的信息整理时使用。
> 日常学习用精简版（[[agent信息整理工作流]]），深入研究用这个。

---

## 工作流全景

```
你提出问题
    │
    ▼
┌─────────────────────────────────────────────────┐
│  Phase 1    确定范围 ── 拆解问题，画出研究地图      │
│  Phase 2    多源搜索 ── 5 个角度并行采集信息         │
│  Phase 3    交叉验证 ── 三方验证，剔除不可靠信息      │
│  Phase 4    结构化   ── 渐进式摘要，组织成可读结构    │
│  Phase 5    输出归档 ── 写入 Obsidian，建立知识链接  │
└─────────────────────────────────────────────────┘
    │
    ▼
一份带来源标注、结构清晰、可检索的学习笔记
```

---

## Phase 1：确定研究范围（Scoping）

### 目标
把模糊的"我想了解 X"变成清晰的研究地图，确保不跑偏、不遗漏。

### 小德会做的事
1. **澄清主题**：如果不明确，会先问你 2-3 个问题界定范围（如：深度？侧重理论还是实践？时间范围？）
2. **拆解子问题**：将一个主题拆成 3-5 个互补的子角度，例如：
   - 宏观框架：这个领域的全貌是什么？
   - 核心机制：关键原理/方法论是什么？
   - 实践案例：有什么公认的案例/项目可以参考？
   - 争议/前沿：有什么不同的观点或最新进展？
   - 对比分析：相似概念之间有什么区别？
3. **确认范围**：把拆解结果展示给你，确认后再进入下一阶段

### 设计依据
- 学术界主流框架（Shi et al., arXiv:2512.02038）将 Deep Research 系统拆分为四大基础组件，其中"Query Planning（查询规划）"是第一环[^1]
- NotebookLM Deep Research（Google, 2025.11）的核心创新就是"先规划研究大纲，再逐节搜索撰写"[^2]
- NVIDIA AI-Q Blueprint（GTC 2026）强调"evidence-grounded planning"——研究计划必须建立在已有知识基础上[^3]

---

## Phase 2：多源搜索与采集（Multi-source Search）

### 目标
从多个独立角度同时搜索，避免单一来源的偏见，覆盖更全面。

### 小德会做的事
1. **并行搜索**：针对 Phase 1 拆出的每个子角度，同时发起搜索，互不干扰
2. **多源优先**：优先采集以下类型（按可信度排序）：
   - **学术综述**（arXiv、顶会论文）——系统性强、有同行评议
   - **官方文档**（引擎文档、设计规范）——一手权威
   - **行业深度文章**（GDC演讲、资深从业者博客）——实战验证
   - **社区共识**（Reddit/HackerNews 高赞、GitHub 高星项目）——众包验证
3. **去重**：跨来源合并重复信息，标注不同来源对同一观点的佐证强度

### 信息来源优先级

| 层级 | 类型 | 示例 | 可信度 |
|------|------|------|--------|
| 第一手 | 学术论文、官方文档 | arXiv、Unity/Unreal 文档 | ⭐⭐⭐⭐⭐ |
| 第二手 | 行业报告、GDC 演讲 | GDC Vault、开发者博客 | ⭐⭐⭐⭐ |
| 第三手 | 高质量社区讨论 | Reddit 精华帖、GitHub Discussions | ⭐⭐⭐ |
| 参考 | 百科类、入门教程 | Wikipedia、YouTube 教程 | ⭐⭐ |

### 设计依据
- Obsidian Research Assistant（nima1313）采用的"memory-first search"策略：先搜索本地知识库，再搜索外部，避免重复研究[^4]
- NVIDIA AI-Q Blueprint 使用 5 个并行专业子代理从不同视角审视同一问题[^3]
- Obsidian Research Assistant 的双通道研究：DuckDuckGo（广度）+ arXiv（深度）[^4]

---

## Phase 3：交叉验证与筛选（Cross-verification）

### 目标
用"三方验证"机制剔除不可靠信息，确保最终笔记的每一条关键信息都有可信来源支撑。

### 小德会做的事
对每一条关键信息，执行以下检查：

1. **来源质量评估**：这条信息来自学术论文还是个人博客？是原文还是转述？
2. **多方交叉验证**：至少 2 个独立来源支持才保留；只有一个来源的观点标记为"待验证"
3. **时效性检查**：信息是否过时？（游戏设计领域：2 年前的"最佳实践"可能已被替代）
4. **立场识别**：是否带有商业推广/个人偏见？（如某引擎官方文章可能偏向自家方案）
5. **事实 vs 观点**：区分"X 游戏用了这个设计"（事实）和"这个设计很好"（观点）

### 验证结果标记
- ✅ **已验证**：2+ 独立来源支持
- ⚠️ **单一来源**：仅一个来源，标记待验证
- ❌ **不可靠**：无来源或来源不可信，不纳入笔记
- 🏷️ **观点**：是作者主观判断而非事实，保留但标注

### 设计依据
- 这是 Deep Research 工作流中最关键的质量控制环节
- ICLR 2026 论文（Salesforce & Microsoft）提出了 8 维度评估框架，发现即使最强的 Deep Research 系统仍有 23-47% 的陈述未经来源充分支撑[^5]
- 这个数据说明：**人工验证环节不可省略**，agent 能做的是帮你筛掉明显的噪声，但关键结论仍需要你过目

---

## Phase 4：结构化整理（Structured Organization）

### 目标
将验证过的信息组织成一份**适合人类学习阅读**的结构化文档，而非信息堆砌。

### 4A 渐进式摘要（Progressive Summarization）
借鉴 Tiago Forte 的第二大脑方法论[^6]：

```
Layer 1: 原始摘录（保留原文关键段落）
    ↓
Layer 2: 加粗关键句（一眼能扫到的核心信息）
    ↓
Layer 3: 高亮核心观点（不超过全文 5%）
    ↓
Layer 4: 用自己的话重写（生成最终笔记）
    ↓
Layer 5: 原子化笔记（拆成独立的知识卡片，方便检索和链接）
```

### 4B 笔记结构模板

```markdown
---
tags: [领域标签, 子标签]
created: YYYY-MM-DD
sources: [来源URL或文献引用]
confidence: high / medium / draft
---

# 标题（一句话概括主题）

## TL;DR（30 秒速览）
- 3-5 条最核心的结论
- 每条一句话

## 1. 核心概念
- 是什么 / 不是什么
- 关键定义

## 2. 核心机制/原理
- 它是怎么运作的
- 有哪些关键环节

## 3. 实践应用
- 业界案例
- 怎么落地

## 4. 争议 / 不同观点
- 有哪些反对意见
- 适用边界是什么

## 5. 延伸阅读
- 相关笔记链接
- 推荐深入阅读的资源

## 来源
[^1]: 来源描述
[^2]: 来源描述
```

### 设计依据
- PKM Vault Master（oalanicolas, 2025）强调"结构应该有机生长，而非预先分类"[^7]
- LLM Wiki（DKR 模式, Karpathy 启发）主张"知识在摄入时处理，而非查询时拼装"[^8]
- Axiomind（yigengjiang）的渐进式披露：MOC → 主题页 → 详细笔记，三层递进[^9]

---

## Phase 5：输出与归档（Output & Archive）

### 目标
将笔记落入 Obsidian，建立与已有知识库的链接，设定复习机制。

### 小德会做的事
1. **文件命名**：`[主题].md`，名称简洁、可检索
2. **Frontmatter 完整**：标签、创建日期、来源、置信度
3. **Wiki-link 链接**：自动识别并链接到 vault 中已有的相关笔记
4. **来源引用**：所有关键信息标注出处，方便回溯
5. **建立 MOC 链接**：如果有相关的 MOC（内容地图），自动添加链接
6. **标记置信度**：
   - `high`：多源验证，引用充分
   - `medium`：有来源但不够充分，需后续补充
   - `draft`：初步整理，待深入

### 归档后的维护
- 新学到相关知识时，更新对应笔记
- 在 INDEX 或 MOC 中记录本次研究
- 重大更新时标注 `updated` 日期

---

## 使用约定

### 你只需说：
- "帮我整理一下暗黑 like 的关卡循环设计" → 自动触发完整五阶段
- "快速搜一下 X" → 精简版（跳过多源交叉验证，单源快速笔记）
- "深入 X" → 完整版五阶段

### 小德会主动做：
- 每个 Phase 完成后向你汇报进展，Phase 4 前确认结构是否满意
- 所有笔记写入前让你预览
- 自动识别 vault 中已有的相关笔记并建立链接

### 质量保障
- Phase 3（交叉验证）是最关键的环节，不省略
- 如果没有找到足够好的来源，会诚实告诉你"现有资料不足，以下是初步结论，建议后续补充"
- 区分"事实"和"观点"，不在笔记中将观点伪装为事实

---

## 方法论来源

[^1]: Shi et al., "A Survey on Deep Research Agents," arXiv:2512.02038, Nov 2025. 四大组件：Query Planning → Information Acquisition → Memory Management → Answer Generation。
[^2]: Google, "NotebookLM adds Deep Research tool," TechCrunch, Nov 2025. 制定研究计划 → 扫描数百网站 → 汇编带引用的报告。
[^3]: NVIDIA, "How NVIDIA Won the Deep Research Benchmark," GTC 2026 Blog. Plan-Gather-Synthesize 核心循环 + 5 并行专业子代理 + 双证据恢复验证节点。
[^4]: nima1313, "Obsidian Research Assistant," GitHub, 2025. ChromaDB 语义库搜索 → DuckDuckGo + arXiv 双通道外部搜索 → 智能链接输出。
[^5]: Salesforce AI Research & Microsoft, "ResearchRubrics," ICLR 2026 Poster. Deep Research 系统仍有 40-80% 引用准确率和 23-47% 未支撑的陈述。
[^6]: Tiago Forte, "Building a Second Brain," 2022. Progressive Summarization 五层信息压缩方法论。
[^7]: oalanicolas, "PKM Vault Master," SkillsMP, 2025. 有机增长的知识管理哲学，反对早期过度分类。
[^8]: vanillaflava, "llm-wiki-skills," GitHub, 2025-2026. Karpathy 的 LLM Wiki 模式的社区实现。
[^9]: yigengjiang, "Axiomind," GitHub, 2025. 七实体分类法，差量优先摄入。
