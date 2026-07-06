# Life in Book — CLAUDE.md

## 项目概况

Life in Book 是一个文学人物心理侧写项目（三层分析：人物心理 → 时代语境 → 作者表达）。内容存储在 Markdown + YAML frontmatter 中，网站基于 Next.js 构建。

## 核心约定

### 文件结构

```
data/works/{work_id}/
├── work.md                  # 作品元信息（章节列表、人物清单）
├── characters/{character_id}/
│   ├── profile.zh-CN.md     # 中文档案（YAML frontmatter + Markdown 正文）
│   └── profile.en.md        # 英文档案
├── era/
│   └── era.zh-CN.md         # 时代语境分析
└── author/
    └── author.zh-CN.md      # 作者表达分析
```

### 存储格式

- Markdown + YAML frontmatter（用 `gray-matter` 解析）
- frontmatter 存放定量数据（大五人格、百分位等）和元信息
- 正文用 Markdown 写定性分析
- 中英文各自独立文件，不是翻译关系

### 心理分析规则

1. 每一条心理推断必须有原文引用支撑（标注章节/回目）
2. 每个分析结论必须标注使用的心理学框架
3. 区分"文本支持的结论"和"合理推测"
4. 定量评分必须锚定在全体已分析人物的分布上（百分位）
5. 免责标注放在页面底部："以上分析基于心理学框架对虚构人物的解读，仅供阅读辅助，不构成临床诊断"

### 剧透四层级

| 级别 | 含义 | 前端表现 |
|------|------|---------|
| `none` | 不涉及剧情信息 | 始终可见 |
| `context` | 涉及场景氛围，不泄露结果 | 未设置进度时折叠 |
| `plot` | 涉及具体情节事件 | 按章节进度折叠 |
| `climax` | 结局、重大转折、死亡 | 双重保护 + 额外确认 |

附加 `cultural_common_knowledge` 布尔字段，为 true 时提示语气降级。

### 译本约定

| 作品 | 中文引用版 | 英文引用版 |
|------|-----------|-----------|
| 红楼梦 | 人民文学出版社 1982（庚辰本） | Hawkes, *The Story of the Stone* |
| 罪与罚 | 上海译文 朱海观/王汶 | Pevear & Volokhonsky (Vintage 1993) |

### 许可证

- 代码 MIT
- 内容 CC BY-NC-SA 4.0

## 当前状态

- 设计文档已定稿：`docs/DESIGN.md`
- 试点书：《红楼梦》《罪与罚》
- 仓库骨架已就绪，内容为占位状态
- 下一步：**Phase 0 原型验证** → 实际写档案

## 关键路径（Phase 0）

1. 撰写《红楼梦》和《罪与罚》的完整三层档案（L1 人物 + L2 时代 + L3 作者）
2. 验证 Markdown + YAML frontmatter 的存储方案
3. 验证剧透四层级的适用性
4. 找读者试用收集反馈
