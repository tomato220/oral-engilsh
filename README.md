# oralenglish-skill

专四（TEM-4）口语思辨陪练 Skill。

## 1. 项目解决什么问题

英语专业学生在备考专四口语时，普遍面临三个问题：

- **没人出话题**：思辨类话题即兴论述不知道练什么、怎么开口。
- **中式英语没人纠**：自己练看不到"中文直译语序、中式搭配、逻辑断层"这些母语负迁移问题，说错了也浑然不觉。
- **缺少反馈闭环**：练完没有逐句的转写、优化和点评，难以形成"开口 → 被纠正 → 再开口"的迭代。

本项目提供一个**纯文本交互式的思辨陪练工作流**：AI 一轮轮抛出英文话题并给出正反参考句型，用户口头作答后，AI 原样转写、给出一版适配专四口语的优化句、并点明中式英语问题，形成即时反馈闭环。

## 2. 主要功能

- **话题式轮番陪练**：每次抛出一个英文思辨 Topic，逐轮推进，不跳步、不一次性给多个话题。
- **正反参考句型**：每轮附带一句肯定立场（For）与一句否定立场（Against）的纯英文开场句型，供用户直接套用。
- **原句转写**：`【我的原句】` 原样转写用户口述英文，不做修正、不补全。
- **优化改写**：`【优化句】` 仅生成 1 版，优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换，适配口头表达，改动核心加粗。
- **简短点评**：`【简短点评】` 点明本次中式英语问题，并说明逻辑、句式、用词地道度。
- **双分支推进**：`【继续】` 基于当前话题深度追问开新一轮；`【重新回答】` 不换话题，等你重新作答后再反馈，循环直到继续。
- **零依赖**：纯文本交互，不涉及网页抓取、PDF、图形界面，无需额外脚本或工具。

## 3. 安装方法

本项目是一个标准 Skill 目录，无第三方依赖、无需编译。

### 方式一：挂载 Skill 目录

将 `oralenglish-skill/` 整个目录（含 `SKILL.md` 与 `agents/`）放入 Agent 环境的 Skill 根目录（例如 `workspace/.user_skills/`），使其作为可加载的 Skill 被识别。

### 方式二：按 Agent 定义加载

按 `oralenglish-skill/agents/openai.yaml`（OpenAI Agents SDK 格式）将 `oralenglish-practice` 加载为 Agent，即可独立使用。

## 4. 使用方法

安装完成后，直接用自然语言发起陪练即可，无需额外配置，例如：

- “用 oralenglish-skill 陪我练专四口语思辨”
- “来一轮口语思辨话题”
- “给我出一个正反立场的英文话题，我来说”

AI 会按固定节奏推进：

1. **开场**：给出英文 Topic + 一句 For（肯定）+ 一句 Against（否定）参考句型，等你作答。
2. **作答后反馈**：依次输出【我的原句】→【优化句】→【简短点评】。
3. **选项**：反馈后给出【继续】·【重新回答】。
4. 按你的选择继续深挖或重新作答。

## 5. 输入输出示例

### 输入（用户发起）

> 陪我练一轮专四口语思辨。

### 输出（AI 开场：Topic + 正反参考句型）

> **Topic**: Should college students take part-time jobs during the semester?
>
> **For**: Working part-time gives students a real taste of the adult world before they graduate.
>
> **Against**: Taking on a part-time job may distract students from their academic focus.

### 输入（用户口头作答）

> I think take part-time job can help student learn more things, and also can earn money. But it will waste time, so I don't know.

### 输出（AI 反馈：原句 + 优化句 + 点评）

> **①【我的原句】**  
> I think take part-time job can help student learn more things, and also can earn money. But it will waste time, so I don't know.
>
> **②【优化句】**  
> I think taking a part-time job **helps students learn more than just textbooks** and **also lets them earn some money**. But it does take up time, so **I'm not entirely sure** whether it's worth it.
>
> **③【简短点评】**  
> 最典型的中式英语是 *"I think take part-time job can help student"* —— 中文"我觉得做兼职能帮学生"直译，英文里 doing 不能省，主语要完整，help sb do sth 的搭配也缺失。逻辑上好处、坏处、犹豫三步都有，但衔接松散；优化句用 and also、but、so 串成更顺的因果链。用词整体口语化，但"learn more things"太泛，改成 learn more than just textbooks 更有内容。

> 选项：【继续】·【重新回答】

## 目录结构

```
D:\oral engilsh\
├── README.md                    # 本说明
└── oralenglish-skill\
    ├── SKILL.md                 # Skill 主文件：完整陪练工作流
    └── agents\
        └── openai.yaml          # OpenAI Agents SDK 的 Agent 定义（开源分发用）
```

## 验证

- 使用官方 `quick_validate.py` 校验通过（frontmatter 与命名合规）。
- 已用科技、教育两类话题演练完整流程（开场 → 反馈三段式 → 继续/重新回答分支），均符合预期。

## License

本项目以 [MIT License](./LICENSE) 开源分发，详见项目根目录 `LICENSE` 文件。
