# h3-playbook-skill

MiniMax H3 视频生成的**单一入口 skill**：官方《使用手册》口径 + 官方 `h3-prompt-writing` 写作契约 + 官方垂类配方 + 实测定论四合一。

## 内容来源

| 来源 | 内容 |
|---|---|
| MiniMax 官方《MiniMax H3 模型 - 使用手册》 | 能力边界、三段式公式、素材标签、踩坑表 |
| 官方 skill `h3-prompt-writing`（`MiniMax-AI/MiniMax-H3`，2026-08-11 版 / commit `a107547`） | T2VA / I2VA / FL2VA / L2VA 字段级最终结构、Ref2VA 六段改写格式（原文逐字节拷贝于 `references/base-en.txt` / `ref-en.txt`） |
| 官方 `skills/` 下 8 个垂类 style skill（2026-08-05 起加入） | 结构/风格分层、参考图窄职责、分镜表列规范、>15s 拼接锁、画面文字与音频策略（提炼于 `references/style-recipes.md`，未逐字搬运）；这 8 个包本身可安装，遇整包需求建议让用户装成独立 skill，判据与命令见 §十 |
| 实测定论（2026-09-28~30，E1~E25 系列） | 分辨率安全点、steps/duration 正交、脸框-细节阶梯、事件丢失规律、链式首尾帧、景别不对称律等（汇总于 `references/field-tested.md`） |

**功能边界**：只讲 H3 本身——提示词结构、生成模式、素材用途、能力边界、踩坑。
ComfyUI 落地（选模型、传参、任务排障）、机器配置与成本不在本 skill。与官方口径冲突时以实测为准。

## 覆盖能力

- 三段式提示词公式：`参考素材说明 + 核心创意 + 画面过程说明`
- 五类生成模式判定与写法差异：**T2VA / I2VA / FL2VA / L2VA / Ref2VA**
- Ref2VA 六段改写格式（`subject_definitions → summary → retention_analysis → detailed_description → overall_soundscape → non_diegetic_music`）
- 参考素材用途标签（`@图片N` / `<Picture N>` 两套编号口径）
- 能力边界：时长 4–15s、分辨率、宽高比、输入上限、语言
- 踩坑表：口型不同步、切镜错乱、文字乱码、莫名 BGM 等
- 垂类配方速查：极简产品广告 / 3D 动画短片 / 纸艺定格 / 拼贴讲解 / 品牌宣传 / MV 排版 / 双人游戏开场 / 手绘发光实拍
- >15s 拆镜与五条连续性锁（H3 单条上限 15 秒）

## 目录结构

```
h3-playbook-skill/
├── SKILL.md                        # 入口：判模式、核心公式、硬规则、自检清单
└── references/
    ├── capability-limits.md        # 能力边界：能不能做、时长/分辨率/宽高比/输入上限
    ├── ref-material-roles.md       # 参考素材用途标签
    ├── skeletons.md                # 三段式完整骨架（含模式差异 + 官方示例）
    ├── pitfalls.md                 # 官方踩坑表与文字乱码对策
    ├── field-tested.md             # 实测定论（分辨率/步数/脸框/事件规律/已封死方案）
    ├── style-recipes.md            # 官方 8 个垂类 skill 的 H3 提示词层提炼（分层/参考图职责/分镜表/拼接/文字音频）
    ├── base-en.txt                 # 官方英文契约原文（T2VA/I2VA/FL2VA/L2VA）
    └── ref-en.txt                  # 官方英文契约原文（Ref2VA 六段格式）
```

## 何时使用

- 写 / 改 / 扩写 H3 视频提示词（任何一种生成模式）
- 判断「这个需求 H3 能不能做」、选时长 / 分辨率 / 宽高比、算输入素材够不够
- 给上传的图 / 视频 / 音频标用途，或设计多素材分工
- 出片有乱码 / 口型不同步 / 切镜错乱 / 莫名多出 BGM，要找原因

**不适用**：Qwen-Image-2.1 出图改图（用 `qwen-image2.1-prompt-writing-skill`）、调用端注册 / 部署 / 排障本身。

## 官方同步

每次更新本 skill 时，顺查官方仓库有无更新：

```bash
curl -s "https://api.github.com/repos/MiniMax-AI/MiniMax-H3/commits?path=skills&per_page=3"
```

最新 sha ≠ `a107547` 即有更新（`skills` 与 `skills/h3-prompt-writing` 两条路径都要看）。官方再更新时：diff 对应文件后同步进本 skill，并升 `skill_version`。

## 版本

`skill_version: 2.8.1`
