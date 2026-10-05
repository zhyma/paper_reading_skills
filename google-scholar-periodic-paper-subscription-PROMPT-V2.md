# Google Scholar 定期论文推送订阅 Prompt V2

## 版本控制（强制）

每次对本 Prompt 文件进行任何更新、修改或修订时，都必须在保存更新版本前将版本号自动递增 1，并同时更新以下两处，二者必须保持一致：

- 一级标题中的版本号：`# Google Scholar 定期论文推送订阅 Prompt V<N>` → `# Google Scholar 定期论文推送订阅 Prompt V<N+1>`；
- 文件名中的版本号：`google-scholar-periodic-paper-subscription-PROMPT-V<N>.md` → `google-scholar-periodic-paper-subscription-PROMPT-V<N+1>.md`。

更新后的文件必须以新版本号另存，不得继续使用旧版本号文件名。

---

## Prompt

检查我已连接的 Gmail 中的 Google Scholar 订阅/提醒邮件，并识别此前任务运行中尚未处理过的论文。

应以“论文”为单位记录处理状态，而不是以“邮件”为单位。不要将检查范围限制为“昨天”“过去 24 小时”或其他固定时间窗口。目标是发现此前尚未检查过的论文，因此同一论文被不同提醒邮件重复推送时，不应被视为新论文。

---

## 1. 论文发现与原文获取

Google Scholar 提醒仅作为论文发现入口。

对于每篇新发现的论文：

1. 打开 Google Scholar 提醒中提供的论文链接。
2. 如果链接可以公开访问论文全文，则尽可能读取原文，并以原文作为主要分析依据。
3. 如果链接指向 publisher 页面、付费墙或其他无法公开访问全文的来源，则进一步搜索是否存在：
   - arXiv preprint；
   - 作者公开提供的 preprint / manuscript；
   - 其他合法公开版本。
4. 如果能够找到公开全文或 preprint，则优先使用该版本进行分析。
5. 只有在无法获取全文或 preprint 时，才退回使用：
   - publisher abstract；
   - Google Scholar snippet；
   - 其他可靠的论文元数据。
6. 不得根据有限信息推断来源中没有明确支持的技术细节。
7. 如果分析依据不是全文，应明确控制结论强度，不要将未验证的信息写成论文已经明确实现或验证的事实。

---

## 2. 每篇论文的信息栏（强制）

每篇论文开始时必须先输出两行信息。

### 第一行：论文信息

格式：

**完整第一作者姓名 et al., Title, Venue Year**

要求：

- 第一作者必须尽可能使用完整姓名，即 given name + family name，不要只写姓，也不要在能够从论文原文确认完整姓名时只写首字母缩写。
- 如果论文只有一位作者，则不加 `et al.`。
- 作者与标题之间使用英文逗号 `, ` 分隔；标题与出处之间同样使用英文逗号 `, ` 分隔。
- 出处尽量写成简洁的 `Venue Year`，例如 `arXiv 2026`、`RA-L 2026`、`ICRA 2026`。
- 示例：`Yijie Wang et al., Reconstruct, Practice, Go Real: Guided Self-Improvement for Embodied Agents, arXiv 2026`。

### 第二行：Scholar 订阅来源与作者单位

格式：

**Scholar 订阅作者：<具体作者姓名>；作者单位：<单位 1>；<单位 2> 等**

要求：

- 必须根据 Google Scholar 提醒邮件明确指出：这篇论文是因为我订阅了哪一位作者而被推送。
- 该作者不一定是论文第一作者，因此不得仅根据第一作者猜测订阅对象；优先以提醒邮件主题中的作者名为依据，并与论文作者列表核对。
- 作者单位优先从论文原文的 author affiliation 获取。
- 最多列出两个单位；如果论文涉及更多单位，在第二个单位之后写“等”。
- 优先确保订阅作者所在单位被包含；如果订阅作者存在多个单位，可列出最多两个。
- 如果无法可靠确认单位，写“未确认”，不要猜测。

---

## 3. 论文分类

将新论文首先分为以下两条研究线。

### A. DLO / deformable-object robotics

关注与 deformable object 和 DLO robotics 直接相关的研究，包括但不限于：

- DLO perception
- DLO representation / modeling
- DLO manipulation
- DLO task planning
- cable / rope / ribbon / strap manipulation
- insertion
- threading
- routing
- tying
- looping
- deformation-aware manipulation
- contact-aware manipulation
- failure detection
- failure recovery
- correction

这一类论文的目的不是判断其“是否值得精读”，而是持续回答：

- 当前 DLO / deformable-object 研究主要在解决什么任务？
- 这些任务采用什么 perception、representation、planning、policy 或 control 方法？
- 当前该研究方向正在使用什么技术路线？

对这类论文，应特别注意区分：

- perception
- state / object representation
- modeling
- planning
- policy
- control
- feedback
- correction / recovery

不要把这些不同环节混合成一个模糊的“method”。

### B. General robot manipulation

用于跟踪当前主流 robot manipulation 学界正在研究什么任务，以及主要采用什么技术路线。关注但不限于：

- visuomotor policy
- imitation learning
- behavior cloning
- diffusion policy
- generative policy
- reinforcement learning
- residual RL
- VLA
- world model
- hierarchical policy
- action chunking
- planning + learned policy
- multimodal perception
- tactile feedback
- force feedback
- closed-loop manipulation
- replanning
- failure detection
- failure recovery
- generalist manipulation

对 general robot manipulation，不仅记录“用了什么方法”，还要重点分析论文内部对技术路线变化的讨论：

- 相比已有方法，具体修改、替换、增加或重新组合了什么？
- 为什么这样改？已有路线存在什么问题或限制？
- 修改试图达到什么目的？
- 作者本人如何看待当前或未来的技术发展方向？

作者对技术趋势的判断只能来自论文中的明确表述，例如 Introduction、Related Work、Discussion、Conclusion 或作者对已有路线局限性的总结。不要根据单篇论文自行推断整个领域趋势，也不要做跨论文趋势总结。

如果论文明显不属于以上两条研究线，则仍保留两行论文信息，但明确写“未纳入 A/B 两类”，并用一两句话说明原因；不要为了套模板强行归类。

---

## 4. 单篇论文信息提取原则

不需要执行完整 paper-reading 流程，也不要生成长篇论文摘要。

目标是使用尽可能短的关键词、短语和技术链条表达论文核心信息。专业术语、模型名、方法名、变量名和常见机器人术语可以保留英文；其余说明默认使用中文。

### 技术路线必须“由整体到细节”（强制）

不要一进入“技术路线”就直接罗列非常细的 input、module、loss、controller 或 rollout 细节。

每篇论文的“技术路线”必须遵循以下顺序：

1. **整体框架**：先用 1–2 句话说明整篇方法总体属于什么路径、核心组织方式是什么。
   - 例如：`整体上是 simulation-based self-improvement 框架，通过在数字环境中发现并修复技能，再部署到真实机器人。`
   - 例如：`整体上是 hierarchical offline RL，通过多时间尺度 value abstraction 解决长时程 goal-conditioned control。`
   - 例如：`整体上将 nominal task execution 与 explicit failure recovery 拆成两个互补模块。`
2. **模块拆分**：再说明整体框架被拆成哪些主要模块或阶段，各模块分别完成什么。
3. **必要细节**：只有对理解方法真正必要时，才进一步给出关键 observation / representation / policy / planning / action / control 链条。

推荐写法：

`整体框架：<一句话概括>`

`主要模块：① <模块 1>；② <模块 2>；③ <模块 3>`

`关键链条：<必要时再写 Input → Representation → Policy/Planning → Action>`

技术路线应优先帮助我先理解“整篇论文在做什么”，再理解“具体怎么做”，而不是从实现细节反推整体方法。

---

## 5. 实验任务提取

无论属于 DLO 类还是 general robot manipulation 类，都必须尽量列出论文中的所有主要实验任务。

不要只写：

- `multiple manipulation tasks`
- `several insertion tasks`
- `various real-world tasks`

而应尽量列出具体任务，例如：

- GPU insertion
- GPU removal
- Ethernet cable plugging
- Ethernet cable unplugging
- peg insertion
- drawer opening
- cable threading
- rope routing
- connector insertion
- knot tying

实验任务只需记录：**任务名称 + 对象 / 动作**。

除非某项信息对理解技术路线本身是必要的，否则不要额外记录成功率、trial 数、GPU 型号、机器人型号、数据规模、训练时长等实验配置。

---

## 6. 输出格式（强制使用竖排两列表格）

为了适配聊天页面宽度，禁止使用需要横向滚动的多列表格。所有论文均使用“左栏 = 字段，右栏 = 内容”的两列表格。

### A. DLO / deformable-object robotics

先输出第 2 节规定的两行论文信息，然后使用：

| 字段 | 内容 |
|---|---|
| 实验任务 | ... |
| Perception / Representation | ... |
| Method / Planning / Control | 先写整体框架，再写主要模块，必要时补充关键技术链条 |
| Feedback | ... |

字段要求：

- **实验任务**：尽量列出所有主要任务，具体到对象与动作。
- **Perception / Representation**：只写理解方法所必需的 sensor / observation / state representation / object representation / geometric or learned representation。
- **Method / Planning / Control**：必须遵守“整体框架 → 模块拆分 → 必要细节”的层级，不得直接从细粒度技术链条开始。
- **Feedback**：说明 open-loop / closed-loop、visual / tactile / force feedback、replanning、correction、failure recovery 等；若论文没有明确说明，写“未说明”。

### B. General robot manipulation

先输出第 2 节规定的两行论文信息，然后使用：

| 字段 | 内容 |
|---|---|
| 实验任务 | ... |
| 技术路线 | 先写整体框架，再写主要模块，必要时补充关键技术链条 |
| 主要技术改动 / 创新 | ... |
| 为什么这样改 / 解决什么问题 | ... |
| 作者对技术趋势的看法 | ... |

字段要求：

#### 实验任务
列出论文中的所有主要实验任务，尽量具体到对象与动作。

#### 技术路线
必须由整体到细节：

- 先说明整篇方法属于什么总体框架或技术路径；
- 再拆分主要模块 / 阶段；
- 最后仅在必要时写具体 `Input / Observation → Representation / Model → Policy / Planning → Action / Control`。

不要一开始就写很长的细粒度 pipeline。

#### 主要技术改动 / 创新
重点写相对于已有技术路线：

- 增加了什么；
- 删除了什么；
- 替换了什么；
- 重新组合了什么；
- 将哪个模块从 A 改成 B。

尽量使用短语，例如：

- `open-loop action chunk → feedback-driven replanning`
- `behavior cloning → diffusion-based action generation`
- `nominal controller + learned residual`
- `vision-only → vision + tactile`
- `task-specific policy → shared generalist policy`

#### 为什么这样改 / 解决什么问题
只提取作者明确说明的设计动机和目标。优先写成：

`已有问题 → 修改目的`

不要自行补充作者没有讨论的动机。

#### 作者对技术趋势的看法
只提炼作者本人对研究路线演进的判断。如果论文没有明确表达相关观点，写：`未明确讨论`。

---

## 7. 去重规则

对论文进行跨邮件、跨运行去重：

- 同一次运行中，不同 Google Scholar alerts 推送的同一论文应合并。
- 不同日期的 alerts 再次推送已经处理过的论文时，不应重复作为新论文分析。
- 明显的标题变体应尽量识别为同一工作。
- arXiv、conference 和 journal version 如果属于同一项研究工作，默认视为同一论文。
- 如果此前处理过的论文出现 substantially revised version、正式发表版本或包含明显新增技术内容的新版本，可以重新记录。
- 对重新出现的新版本，必须明确标注为已有工作的更新版本，而不是作为完全独立的新论文处理。

---

## 8. 不需要执行的内容

不要：

- 给出“精读 / 浏览 / 可跳过”等阅读建议；
- 给论文打分；
- 生成 Top-N 推荐；
- 生成“今日最值得看”或“本周最值得看”；
- 对 general robot manipulation 做跨论文趋势总结；
- 为了补齐表格而猜测论文没有报告的信息；
- 将 abstract 或 Google Scholar snippet 中没有的信息视为事实；
- 为每篇论文生成冗长摘要；
- 使用需要横向滚动才能看全的宽表格。

---

## 9. 总体目标

该任务不是论文推荐器，而是持续运行的科研信息监控与技术路线记录工具。

通过持续处理新的 Google Scholar 推送，分别回答：

### DLO / deformable-object robotics
- 最近在研究什么任务？
- 使用什么 perception / representation？
- 使用什么 planning / policy / control 方法？
- 是否使用 feedback、replanning、correction 或 recovery？

### General robot manipulation
- 最近在研究什么具体 manipulation task？
- 整体采用什么技术框架？
- 框架内部拆分为哪些主要模块？
- 相对于已有方法具体改了哪里？
- 为什么这样改，试图解决什么问题？
- 作者本人如何描述当前技术路线的变化与未来方向？

输出应保持高度压缩，但必须先给出整体方法结构，再展开必要细节，使我能在不横向滚动页面的情况下快速理解论文的技术结构，并持续跟踪 DLO robotics 与 general robot manipulation 的研究发展。
