---
name: paper-reading-unified
description: 结构化阅读、拆解和总结学术论文/PDF。采用“通用论文阅读 → 机器人领域扩展 → DLO 专项扩展”的分层结构，以问题抽象、输入/输出、表征/模型、方法链、实验证据、局限和研究脉络为共同核心；对机器人论文进一步分析 perception、state、planning、policy、control、feedback 与 hardware；对 DLO（deformable linear object）论文进一步分析 cable、wire、rope、string、suture、catheter、elastic rod、wire harness、flexible flat cable、ribbon 等对象的 modeling、perception、planning、manipulation 与 control。默认中文解释并保留英文术语。精读输出必须严格遵守本文件指定 Markdown 模板，并同时生成内容一致的可下载 .md 副本。
---

# Unified Paper Reading Skill V4

把论文转化为可继续研究、可横向比较、可直接保存为研究笔记的结构化总结，而不是简单复述 Abstract / Introduction / Method / Conclusion。

本 Skill 按照 **从抽象到具体、从通用到专精** 的顺序组织：

1. **通用论文阅读层**：适用于所有论文；
2. **机器人专业层**：仅在论文核心属于 robotics / control / autonomous systems 时叠加；
3. **DLO 专项层**：仅在论文核心涉及 deformable linear object 时，在通用层和机器人层之上继续叠加。

继承关系为：

`通用规则 → 机器人扩展 → DLO 扩展`

后一级只补充本领域特有的信息，不重复前一级已经定义的共同规则。若某项内容已经能由通用层处理，应优先保留在通用层，不在机器人或 DLO 层重复定义。

---

# 1. 最高优先级规则

以下规则优先于后文所有建议性规则。

1. **版本控制（强制）。** 每次对本 Skill 文件进行任何更新、修改或修订时，都必须在保存更新版本前将版本号自动递增 1，并同时更新以下两处，二者必须保持一致：
   - 一级标题中的版本号：`# Unified Paper Reading Skill V<N>` → `# Unified Paper Reading Skill V<N+1>`；
   - 文件名中的版本号：`paper-reading-unified-SKILL-V<N>.md` → `paper-reading-unified-SKILL-V<N+1>.md`。
   更新后的文件必须以新版本号另存，不得继续使用旧版本号文件名。例如：修改 V3 时，输出必须为标题 `# Unified Paper Reading Skill V4` 且文件名为 `paper-reading-unified-SKILL-V4.md`。
2. **论文/PDF 是主要证据来源。** 不得用常识、同领域惯例或模型记忆补全论文没有报告的事实。
3. **严格区分四类信息：**
   - **论文事实**：正文、图表、公式、附录直接支持；
   - **作者主张**：作者的解释或结论，但实验未必充分证明；
   - **推断**：根据论文证据作出的分析，必须明确标记为推断；
   - **疑问**：需要进一步阅读、复现或外部资料确认的问题。
4. 论文没有提供的信息必须写 **“未说明” / “未报告” / “无法从当前 PDF 确认”**。不得为了填满模板而臆造。
5. 默认中文解释，保留准确的英文术语、方法名、任务名、变量名和算法名。
6. 所有影响核心判断的内容尽量附 **PDF 页码**；必要时同时标注 Section、Figure、Table、Equation。若 PDF 页码与论文印刷页码不同，应明确区分。
7. 先建立论文的研究坐标，再进入网络、算法或实现细节：
   - 在真实世界或研究领域中有什么用；
   - 论文真正求解的抽象问题是什么；
   - 输入和输出是什么；
   - 用什么表征、模型和方法；
   - 方法如何从输入走到输出；
   - 实验是否真正支持作者的主张。
8. 用实验评价贡献，而不是重复作者宣传语。实验细节、具体数据、baseline、ablation、failure 和 generalization 应放在详细分析部分，不应塞入结构化总结表格。
9. 作者明确承认的局限、根据证据推得的局限、复现障碍和自己的疑问必须分开。
10. **结构化总结表格是“索引层”，不是“细节层”。** 表格单元格应尽可能使用 **1–2 个短语**；必要时可使用多个短语，但应保持精简；只有无法用短语准确表达时才允许使用 **一句话**。不得在表格中堆叠解释、实验数字或长句。
11. **精读任务的最终输出必须严格遵守本 Skill 对应模板，字段顺序不得自行重排或省略。** 不适用或论文未报告的字段仍保留，并填写“不适用”或“未说明”。
12. **每次完成精读总结后，必须额外生成一个 `.md` 文件供用户下载。** 文件正文必须与聊天中给出的正式论文总结保持一致，不得只生成简版、提纲或不同格式的副本。

---

# 2. 阅读任务识别与层级选择

先识别用户要求的是：

- 单篇结构化精读；
- 快速筛读；
- 复现导向阅读；
- 批判性评估；
- 多论文对比；
- 某一研究方向的研究地图或综述。

若用户没有指定，默认执行 **“单篇结构化精读 + 可比较摘要”**。

随后判断论文所属层级：

1. **所有论文**：执行第 3–4 节通用规则；
2. **机器人核心论文**：在通用规则上叠加第 5–6 节；
3. **DLO 核心论文**：先执行通用规则和机器人规则，再叠加第 7–8 节。

如果机器人或 DLO 仅是一个验证案例，而不是论文核心研究对象，应明确指出，不自动启用完整专业模板。

---

# 3. 通用论文阅读框架

本节适用于所有论文。机器人和 DLO 论文也必须先完成本节，再进入专业扩展。

## 3.1 建立研究坐标

优先回答：

1. **Application / context**：在真实世界或研究领域中有什么用？
2. **Problem abstraction / research question**：论文真正求解什么抽象问题？
3. **Gap and contribution**：已有工作缺什么，本文改变了哪一环？
4. **Input / data / observation**：方法接收什么信息？
5. **Output / prediction / action**：方法最终产生什么？
6. **Constraints / success condition**：什么条件限制方法，什么算成功？
7. **Key assumptions / boundary conditions**：方法成立依赖什么前提？

不要把应用场景、问题抽象、方法类别和实验场景混为一谈。

## 3.2 通用分析镜头

### 算法、机器学习与 AI

检查：

- input、label/supervision、output、objective；
- representation、architecture、inductive bias、loss、optimization；
- training data、split、augmentation、pretraining、data leakage；
- training 与 inference 的区别；
- baseline、公平性、ablation、compute、parameter count、latency、sample efficiency；
- OOD generalization、robustness、calibration、failure cases、interpretability；
- learned model、model-free policy、end-to-end 不得混用。

### 系统、工程与应用论文

检查：

- system requirements；
- modules 与 interfaces；
- design decisions；
- scientific novelty vs engineering integration；
- throughput、latency、resources、reliability、maintainability；
- deployment constraints；
- 局部模块提升是否带来端到端收益。

### 综述、系统综述与元分析

检查：

- scope、search range、inclusion/exclusion、time boundary；
- taxonomy quality、evidence grading、heterogeneity、publication bias；
- research gaps。

目标是重建领域结构，而不是逐篇摘要堆叠。

### 立场、观点与概念论文

检查：

- 核心命题和定义；
- argument chain；
- evidence；
- implicit assumptions；
- counterexamples 和 alternative explanations；
- 可检验含义。

## 3.3 重建通用方法链

优先整理为：

`输入/观测 → 状态或表征 → 模型/核心机制 → 求解/推断/规划 → 输出 → 反馈或更新`

需要明确：

- 模型属于 analytic / physical / statistical / learned / rule-based / hybrid 中哪一类；
- learning stage 和 inference/execution stage 分别需要什么；
- 多层系统中的模块及接口；
- feedback 来源、时机和更新条件；
- 关键公式、变量、伪代码、图表和真正影响方法理解的超参数。

## 3.4 用实验检验主张

详细分析中提取：

- dataset / object / environment / hardware / software；
- sample size / task scale；
- baseline / ablation / metric / success criterion；
- 最能支撑主要结论的 quantitative results 和 qualitative observations；
- failure case / recovery / uncertainty；
- 哪些主张得到实验支持，哪些仍未充分验证。

**具体数据属于本节，不属于结构化总结表格。**

## 3.5 分层写局限与疑问

至少分为：

- 作者明确承认的局限；
- 根据假设、实验设计或结果可推得的局限（明确标记“推断”）；
- reproduction obstacles；
- generalization risks；
- open questions / 待核实问题。

## 3.6 放回研究脉络

记录：

- 最接近的前置工作；
- 真正新增部分；
- 依赖的 model / data / tool / prior；
- 可以和哪些后续方法或问题组合。

连续阅读同一方向论文时，应保持一致的分类轴，便于横向比较。

## 3.7 通用证据表达规则

- 短原文只在需要固定 definition、assumption、contribution、limitation、state/action、success condition 等关键信息时引用，并附定位。
- 优先使用“作者声称……”“论文实验显示……”“从……可以推断……”等措辞体现证据等级。
- 若 Abstract、正文、图表或 Appendix 不一致，应明确指出冲突和各自位置。
- 数学符号保持原义；解释关键变量在系统中的作用，而不是机械转写公式。

---

# 4. 通用输出与结构化总结规则

## 4.1 结构化总结表格的功能

结构化总结表格只用于提供一眼可读的论文索引，回答：

- 这篇论文用于什么场景；
- 把问题抽象成什么；
- 输入是什么；
- 用什么模型/表征/方法；
- 输出是什么；
- 是否有反馈；
- 大致怎么验证；
- 最大限制是什么。

它**不负责解释为什么、如何实现、实验结果是多少**。这些内容必须放入表格之后的详细章节。

## 4.2 表格单元格压缩规则（强制）

每个单元格按照以下优先级填写：

1. **一个短语**；
2. **两个短语**，用 `；` 分隔；
3. 必要时使用少量短语，但避免枚举过多；
4. 若短语无法准确表达，最多写 **一句话**。

优先使用类别词、任务词、模态词、模型族或模块名，不要写解释性段落。

### 推荐风格示例

| Category | 推荐写法 |
| --- | --- |
| Application / context | `工业装配`；`手术`；`食品工业` |
| Problem abstraction | `目标检测`；`轨迹预测`；`插入`；`形状控制` |
| Input / observation | `RGB 图像`；`彩色点云`；`6-DoF 力/力矩` |
| Input + processing | `RGB 图像；DINO`；`深度图；CNN`；`proprioception；MLP` |
| Representation / model | `model-based；multi-link`；`data-driven`；`knot theory` |
| Method | `optimization-based`；`behavior cloning`；`diffusion policy` |
| Output | `类别标签`；`3D pose`；`joint action` |
| Feedback | `closed-loop vision`；`open-loop` |
| Evaluation setting | `real robot；tabletop`；`simulation` |
| Limitations | `occlusion-sensitive`；`manual initialization` |

### 禁止或尽量避免

- 在表格中写成功率、误差值、数据集大小、运行时间等具体数字；
- 在单元格中解释算法流程；
- 把多个实验结论压进一格；
- 用完整段落替代标签化总结；
- 把论文没有明确报告的信息用常识补齐。

## 4.3 通用单篇论文模板

以下结构是所有精读输出的基础模板。机器人和 DLO 论文在继承本模板的基础上，按后文规则替换专业部分。字段无信息时填写“未说明/未报告/不适用”。
首行"##"后的"论文标题"用实际论文标题进行替换

```markdown
## 论文标题
<big>第一作者，机构，会议/期刊/ArXiv 年份</big>
第一作者姓氏, et al., 论文标题, 会议缩写/期刊缩写/ArXiv 年份

### 一句话定位
- 在【应用/领域】中，把【问题】抽象为【任务】，用【核心方法】实现【目标】。

### 结构化总结
| Category | Summary |
| --- | --- |
| Application / context | |
| Problem abstraction / research question | |
| Gap / contribution | |
| Input / observation / data | |
| Representation / model | |
| Method / inference / planning | |
| Output / action | |
| Feedback / online-offline | |
| Evaluation setting | |
| Limitations / failure modes | |

### 问题抽象
- 应用问题：
- 实际求解任务：
- 输入、输出、约束与成功条件：
- 关键假设：

### 方法链
`输入 → 表征/状态 → 模型或核心机制 → 求解/规划 → 输出 → 反馈`

- 关键变量/模块：
- 训练阶段：
- 推理或执行阶段：
- 多层结构与接口：

### 实验与证据
- 实验设置：
- Baseline / ablation：
- 指标与主要结果：
- 结果支持了什么：
- 尚未验证什么：

### 局限与开放问题
- 作者明确承认：
- 可由证据推断：
- 复现障碍：
- 我的问题：

### 研究脉络
- 前置/最接近工作：
- 真正新增之处：
- 可与哪些方法或问题组合：
```

---

# 5. 机器人专业扩展

本节只补充机器人领域特有的信息。通用论文阅读规则继续全部生效。

当论文核心属于 robotics、robot manipulation、motion planning、control、autonomous systems、robot learning、embodied manipulation 等方向时，启用本节。

## 5.1 机器人研究坐标

在通用研究坐标之外，额外回答：

- robot / platform；
- end-effector / gripper / tool；
- environment / object / fixture；
- sensors；
- state / observation；
- action space；
- contact / dynamics assumptions；
- task success condition；
- simulation / real robot。

## 5.2 机器人系统链

按照论文实际存在的层级重建：

`传感输入 → perception / state estimation → task / symbolic planning → motion / trajectory / policy → controller → robot action → feedback / replanning / recovery`

不得为了填满链条而虚构论文不存在的层级。

重点区分：

- perception 与 state estimation；
- task planning 与 motion planning；
- trajectory generation 与 low-level control；
- policy output 与最终 robot command；
- open-loop 与 closed-loop；
- offline planning/training 与 online execution；
- replanning 与 failure recovery。

## 5.3 机器人感知与状态

记录：

- modality：RGB、stereo、RGB-D、depth、point cloud、tactile、force/torque、proprioception、audio、hybrid；
- processing method：traditional CV、registration/tracking、CNN、ResNet、ViT、DINO、SAM、Transformer 等；
- output：mask、keypoints、pose、geometry、state、contact、force、semantic label 等；
- timing：initial observation、continuous tracking、visual servoing、event-triggered sensing、active perception；
- assumptions：calibration、known CAD、marker、lighting、occlusion、sensor noise 等。

不得把 simulation ground-truth state 写成一种感知方法，应标记为 simulator-provided state / ground truth。

## 5.4 机器人 planning / policy / control 层级

| Layer | Typical output | Examples |
| --- | --- | --- |
| Task / symbolic | subgoals、primitive sequence | PDDL、LAMA、VLM/LLM plan |
| Manipulation | grasp、regrasp、skill parameters | TAMP、optimization |
| Motion / trajectory | path、trajectory、pose sequence | RRT/RRT*、A*、spline、IK |
| Policy | EE/joint action、skill parameters | RL、IL、diffusion policy |
| Control | torque、velocity、position command | MPC、MPPI、impedance、visual servo、PD/LQ |

若论文声称 end-to-end，仍必须列清：

- observation；
- action；
- training data；
- execution-time feedback；
- 最终送给机器人的是 joint / Cartesian position、velocity、torque 还是其它命令。

## 5.5 机器人实验与系统证据

在通用实验检查之外，详细记录：

- robot model / DOF；
- gripper / tool；
- camera / tactile / F-T sensor；
- calibration；
- simulator；
- real-world deployment；
- control frequency / system latency（若报告）；
- demonstrations / transitions / rollouts（若涉及 learning）；
- success criterion；
- failure recovery；
- hardware dependency；
- sim-to-real gap。

具体型号、频率、成功率、样本量等数字写在详细实验部分，不写进结构化总结表格。

## 5.6 机器人领域常见分类错误

- neural network 不等于 model-free；
- learned dynamics / forward model 属于 data-driven model-based；
- observation-to-action policy 才通常属于 model-free policy；
- end-to-end 不代表没有内部 representation；
- robot 在运动不代表任务必须属于 dynamic manipulation；
- motion planning、policy 和 controller 不得混为一层；
- task success 与 controller tracking accuracy 不得混为同一指标。

---

# 6. 机器人论文输出扩展

机器人核心论文继续使用第 4.3 节通用模板，但用本节内容替换其中对应部分。其余通用章节保持不变。

## 6.1 机器人结构化总结替换表

表格仍严格遵守第 4.2 节的短语化规则。

```markdown
### 结构化总结
| Category | Summary |
| --- | --- |
| Application | |
| Problem abstraction | |
| Robot / setup | |
| Input / observation | |
| State / representation | |
| Model / method | |
| Planning / policy | |
| Control / action | |
| Feedback / timing | |
| Evaluation setting | |
| Problems / limitations | |
```

推荐粒度示例：

- `Application`：`工业装配`
- `Problem abstraction`：`peg insertion`；`bimanual manipulation`
- `Robot / setup`：`dual-arm；parallel gripper`
- `Input / observation`：`RGB；proprioception`
- `State / representation`：`keypoints`；`latent state`
- `Model / method`：`behavior cloning；Transformer`
- `Planning / policy`：`joint-space policy`
- `Control / action`：`joint position`
- `Feedback / timing`：`closed-loop；camera feedback`
- `Evaluation setting`：`real robot；tabletop`
- `Problems / limitations`：`demonstration-dependent`

## 6.2 机器人“问题抽象”替换部件

```markdown
### 问题与系统边界
- 实际应用：
- 机器人任务定义与成功条件：
- Observation / state / action：
- Robot / environment / contact assumptions：
```

## 6.3 机器人“方法链”替换部件

```markdown
### 方法链
`传感输入 → perception / state → planning / policy → trajectory / action → controller → robot execution → feedback`

- 感知与状态：
- Planning / policy：
- Control / action：
- 训练阶段：
- 实机执行阶段：
- Feedback / replanning / recovery：
```

---

# 7. DLO 专项扩展

本节是机器人专业层之上的更具体分支，只定义 DLO 特有内容。第 3–6 节规则继续全部生效。

当论文核心对象或核心任务涉及以下对象时，自动启用本节：cable、wire、rope、string、thread、suture、shoelace、wire harness、flexible flat cable、elastic rod、ribbon、catheter 或其它可视作 deformable linear object 的细长柔性对象。

如果 DLO 只是论文中的一个验证案例而非核心研究对象，必须明确指出，不自动启用完整 DLO 模板。

## 7.1 DLO 研究链位置

先判断论文主要解决：

- Modeling / simulation；
- Perception / state or parameter estimation；
- Manipulation / motion planning / control；
- Integrated system。

## 7.2 DLO application 与 problem abstraction

在机器人研究坐标上进一步记录：

1. **Application**：工业装配、家务、医疗/手术、汽车/航空线束等；
2. **Task abstraction**：grasping、cable following、insertion、routing、winding、shaping、knotting/unknotting、untangling、suturing、catheter insertion、dynamic rope manipulation 等；
3. **Dynamics**：quasi-static 或 dynamic；
4. **Spatial boundary**：2D / 2.5D / 3D / in-air；
5. **Contact / topology**：free space、fixture contact、self-contact、environment contact、topological change；
6. **Primitive vs composite task**：基础 primitive 与长时程组合任务分开记录。

机械臂发生运动不等于 dynamic manipulation。只有当惯性、振动或高速运动是任务机理的一部分时，才标为 dynamic。

## 7.3 DLO 对象属性

只记录会改变方法或实验结论的属性：

- extensibility；
- bending / torsional stiffness；
- elastic rebound；
- friction；
- diameter / width；
- single / multiple / interlinked / branched DLO；
- single-/double-end fixed；
- rigid connector / aglet / pin；
- length / material / physical parameters 是否已知或在线估计。

## 7.4 DLO task taxonomy

### 基础 primitives

grasp / pick / place / release / regrasp / handover / cable following / sliding / insert / pull / stretch / twist / cage / pinch / rotate / swing / whip。

### 复合任务

- **Insertion**：端点或 pin 穿入 hole / eyelet / connector；
- **Routing**：按指定顺序或方向经过 fixture / clip / peg / region；
- **Winding**：围绕物体形成一圈或多圈接触；
- **Shaping**：使整体或局部形状接近目标形状；
- **Knotting / unknotting / untangling**：改变或简化 crossing / topological state；
- **Suturing**：可能同时含 insertion、looping、winding、knotting；
- **Catheter insertion**：受限空间推进并控制位置、方向和力；
- **Dynamic manipulation**：利用惯性完成 vaulting、knocking、weaving、casting、dynamic knotting 等。

Insertion、routing、winding、knotting 可以共享 primitive，但成功条件和 topology/contact constraints 不同，不得合并成同一任务类别。

## 7.5 DLO 模型与表征

回答两个核心问题：

1. **是否显式建模？**
2. **模型在系统中用于什么？**

| Family | Typical representations | 必须追问 |
| --- | --- | --- |
| Physical | mass-spring、elastic/discrete/Kirchhoff rod、multibody、FEM、PBD | 参数、边界条件、实时性、误差 |
| Geometrical | centerline、curve、spline、segments、particles、vertices/edges、keypoints | 是否表示宽度、长度、曲率、扭率 |
| Topological | crossings、Reidemeister moves、P-data、H-signature、linking number、grasp-loop relation | topology 覆盖 DLO、environment 或 robot 的哪些部分 |
| Jacobian / local | deformation Jacobian、local linearization | 局部有效域、在线更新 |
| Data-driven model | learned forward/inverse/dynamics/state-action model | training distribution、state/action、horizon |
| Model-free policy | observation-to-action RL/IL/diffusion policy | feedback、data、generalization |
| Hybrid | analytic/physical prior + learning/residual/adaptation | 各部分接口和依赖 |

通用分类规则继续生效：

- learned dynamics / forward model = **data-driven model-based**；
- observation-to-action policy 才通常属于 **model-free**；
- neural network 本身不能决定 model-based / model-free；
- physical prior + neural network 或 analytic model + residual learning 应标为 hybrid。

## 7.6 DLO 感知专项信息

机器人感知规则见第 5.3 节。本节只补充 DLO 特有的 perception output 和 failure sources。

重点记录：

- DLO output：mask、skeleton、centerline、spline、keypoints、endpoints、crossings/knot、topology、shape、material property、tension；
- geometry relation：DLO 与 fixture / obstacle / robot / gripper 的相对关系；
- DLO-specific assumptions：thin structure、self-occlusion、crossing overlap、depth noise、marker、manual annotation；
- tracking 是否需要保持 curve / point correspondence；
- 是否能处理 self-contact、multiple DLO 或 branched structure。

## 7.7 DLO planning / manipulation / control 专项信息

机器人 planning / policy / control 的通用层级见第 5.4 节。本节额外检查：

- 是否规划 robot configuration、DLO shape space，或两者耦合；
- grasp / regrasp / contact point 如何选择；
- fixture order 或 topology constraint 如何进入规划；
- DLO state 是否在线更新；
- deformation model 是否参与 planning/control；
- recovery 是否针对 slack、slip、entanglement、misinsertion 等 DLO failure。

## 7.8 Shape control 单独检查

只有当论文目标是真正控制 DLO 整体或局部形状时，才标记 shape control。记录：

- target shape representation；
- error metric；
- grasp / action point selection；
- model-based / Jacobian-based / data-driven / model-free / hybrid；
- single-step / multi-step；
- local / global；
- obstacle / contact；
- closed-loop。

Routing、insertion 或 knotting 中形状发生变化，并不自动等于 shape control。

## 7.9 DLO 实验与失败模式

在机器人实验检查基础上，额外提取：

- object material / length / diameter / width / stiffness / connector；
- fixture / task board / obstacle；
- failure：rebound、slip、slack、entanglement、occlusion、crossing merge、excessive tension、material damage、misdetection；
- generalization：不同 DLO、layout、task length、background、sensor condition；
- 是否依赖 marker、manual fixture annotation、pre-straightening、manual stop 等人工条件；
- 是否只验证一个 primitive，却宣称适用于长时程任务。

具体数值继续只写在详细实验部分，不写入结构化总结表格。

## 7.10 DLO 分类易错点

- “static manipulation”在很多 DLO 文献中实际指 quasi-static；按作者定义说明；
- 系统整体可 quasi-static，但包含 swing 等 dynamic primitive；两层分别记录；
- vision 只用于 initial grasp、fixture localization 或 execution feedback 时，必须写清作用阶段；
- 路径规划可能只规划 robot configuration、只规划 DLO shape space，或两者耦合；必须区分；
- topology representation 与 geometry representation 不得混为一类；
- shape change 不等于 shape control。

---

# 8. DLO 论文输出扩展

DLO 核心论文继承通用模板和机器人模板，但用本节替换对应的专业部分。

## 8.1 DLO 一句话定位替换部件

```markdown
### 一句话定位
- 该论文在【应用】中，把 DLO 问题抽象为【任务 + dynamics / spatial / contact 条件】，通过【核心表征/模型】和【规划/控制方法】完成【目标】。
```

## 8.2 DLO 结构化总结替换表

严格遵守第 4.2 节短语化规则。尤其不得在 `Experiment` 中写具体成功率、误差、样本量或运行时间。

```markdown
### 结构化总结
| Category | Summary |
| --- | --- |
| Application | |
| Problem abstraction | |
| DLO object / setup | |
| Input / perception | |
| DLO state / representation | |
| DLO model | |
| Planning / policy | |
| Manipulation / control | |
| Feedback / timing | |
| Shape control | |
| Evaluation setting | |
| Problems / limitations | |
```

推荐粒度示例：

- `Application`：`线束装配`；`手术`
- `Problem abstraction`：`routing；quasi-static；3D`；`knotting；dynamic`
- `DLO object / setup`：`single cable；one-end fixed`
- `Input / perception`：`RGB-D；centerline tracking`
- `DLO state / representation`：`spline centerline`；`topology graph`
- `DLO model`：`model-based；elastic rod`；`data-driven`
- `Planning / policy`：`topology planning`；`diffusion policy`
- `Manipulation / control`：`regrasp；position control`
- `Feedback / timing`：`closed-loop vision`
- `Shape control`：`yes；Jacobian-based` 或 `not a target`
- `Evaluation setting`：`real robot；dual-arm`
- `Problems / limitations`：`occlusion；manual initialization`

## 8.3 DLO “问题与任务边界”替换部件

```markdown
### 问题与任务边界
- 实际应用：
- DLO 任务定义与成功条件：
- Primitive / composite task：
- Dynamics / spatial / contact / topology boundary：
- 对象与固定条件：
```

## 8.4 DLO “方法链”替换部件

```markdown
### 方法链
`传感输入 → DLO state / representation → model → planning / policy → primitive / trajectory / action → controller → feedback`

- 感知与状态：
- DLO 建模/表征：
- Planning / manipulation：
- Control / action：
- 训练阶段：
- 实机执行阶段：
- Feedback / replanning / recovery：
```

## 8.5 DLO “实验与方向关系”补充部件

在通用 `### 实验与证据` 之后继续保留：

```markdown
### 与 DLO 方向的关系
- 相比前置工作：
- 可归入的 task / model / perception / planning 类别：
- 可与哪些模块组合：
```

---

# 9. 其它输出模式

## 9.1 快速筛读

只有用户明确要求“快速筛读 / 快速判断是否值得读”时使用：

```markdown
- 一句话定位：
- 与当前课题的相关度：高 / 中 / 低；理由：
- 值得精读的章节、图、表或公式：
- 方法关键词：
- 主要证据：
- 最大局限：
- 是否进入对比表：是 / 否
```

## 9.2 多论文对比

用户要求比较多篇论文时：

1. 先分别建立每篇论文的基本研究坐标；
2. 使用一致的分类轴；
3. 表格仍遵守短语化规则；
4. 具体数字放在专门的 quantitative comparison 部分，不塞入概览表；
5. 必须指出哪些论文实际上求解不同子问题，不能因为共享关键词就直接比较。

## 9.3 复现导向

复现导向信息追加在默认精读之后，不得替代默认总结。重点包括：

- code / dataset availability；
- dependencies；
- hardware；
- calibration；
- training recipe；
- hyperparameters；
- preprocessing；
- evaluation procedure；
- missing implementation details；
- reproducibility risks。

---

# 10. `.md` 副本生成规则（强制）

完成单篇精读、多论文对比或复现导向总结后：

1. 先生成符合对应模板的正式 Markdown 总结。
2. 将**同一份正式总结**写入一个 `.md` 文件，不得生成内容缩水的副本。
3. 文件编码使用 UTF-8。
4. 文件名优先采用：
   - `<FirstAuthorSurname>_<ShortTitle>_<Year>_paper_note.md`
   - 若无法可靠得到作者/年份，则使用 `<PDF原文件名去扩展名>_paper_note.md`。
5. 文件名中的 `/ \\ : * ? " < > |` 等不安全字符替换为 `_`。
6. 聊天回答中必须提供该 `.md` 文件的可下载链接。
7. 如果运行环境确实无法创建文件，必须明确说明限制；不得声称已生成下载文件。
8. `.md` 文件不得包含仅供模型内部执行的说明、检查清单或本 Skill 文本，只包含用户需要保存的论文总结。

---

# 11. 论文标题与笔记标题规则

若来源信息足够，论文标题区第二行严格使用：

`第一作者姓氏, et al., 论文标题, 会议缩写/期刊缩写/ArXiv 年份`

例如：

`Kim, et al., Gaze-Based Dual Resolution Deep Imitation Learning for High-Precision Dexterous Robot Manipulation, ICRA 2021`

不得因为信息不确定而猜测 venue；无法确认时明确标注“venue 未确认”。

---

# 12. 完成前检查

## 12.1 所有论文

- 是否先回答 Application / context？
- 是否明确 Problem abstraction / research question？
- 是否从 input 一路追踪到 output？
- 是否分清 representation、model、method 和 output？
- 是否分清 training 与 inference/execution？
- 是否用实验而不是作者宣传语评价贡献？
- 是否分清论文事实、作者主张、推断和疑问？
- 是否把未报告的信息明确写为未说明，而非补全？
- 结构化总结表格是否主要由短语组成？
- 表格是否避免了成功率、样本量、误差值、runtime 等具体数字？
- 详细数据是否放到了“实验与证据”等后续章节？
- 是否严格保留了对应模板的标题、表格与字段顺序？
- 是否已经生成与正式总结内容一致的可下载 `.md` 副本？

## 12.2 机器人论文额外检查

- 是否写清 robot / gripper / sensors / environment？
- 是否区分 observation、state 和 action？
- 是否能从 perception 追踪到 planning/policy、control 和 robot command？
- 是否区分 task planning、motion planning、policy 和 controller？
- 是否说明 online/offline、open/closed loop、feedback、replanning 和 recovery？
- 是否区分 simulation 与 real robot？

## 12.3 DLO 论文额外检查

- 是否从 Application 走到具体 DLO task abstraction？
- 是否区分 quasi-static/dynamic、primitive/composite task、2D/2.5D/3D、contact/topology？
- 是否说明 DLO 如何表示、是否显式建模、模型在系统何处使用？
- 是否写清 DLO-specific perception output 和 assumptions？
- 是否说明规划的是 robot、DLO，还是 coupled robot-DLO state？
- 是否正确区分 model-based/model-free/hybrid 与 physical/geometrical/topological/data-driven？
- 是否记录 failure/recovery 和 generalization boundary？

---

# 13. 推荐执行指令

当本 `SKILL.md` 与待阅读 PDF 一起提供时，执行者应：

- 不再要求用户重复说明模板；
- 先执行通用阅读层；
- 自动判断是否需要叠加机器人专业层；
- 自动判断是否需要继续叠加 DLO 专项层；
- 默认做结构化精读；
- 结构化总结表格只写最简短的类别性信息；
- 具体方法解释、实验数字和证据放入后续详细章节；
- 关键判断标页码；
- 未报告信息明确标注；
- 完成后生成完全一致的 `.md` 下载副本；
- 若用户另有明确阅读重点，在不破坏模板和证据纪律的前提下额外展开。
