# Life in Book · 设计文档

> 三层分析框架：人物心理 → 时代语境 → 作者表达
> 读懂一个人物，理解一本书。

---

## 一、项目哲学

### 1.1 我们在做什么

一本小说是一个多层嵌套的谜题。

最表层是情节——**人物做了什么**。往下一层是心理——**人物为什么这样做**。再往下一层是时代——人物为什么**只能**这样做，什么社会力量在挤压他们的选择空间。最底层是作者——写这本书的人当时在经历什么、在愤怒什么、在渴望什么，以至于要创造一个虚构世界来承载这些。

这三层不是独立的。一个人物的心理创伤，根源可能在时代的结构性暴力；一个时代的荒诞，很可能就是作者每天在饭桌和办公室里忍受的东西。所以这个项目做三层分析，一层套一层：

| 层级 | 分析对象 | 核心问题 |
|------|---------|---------|
| L1 · 人物侧写 | 虚构人物 | 这个人的心理构造是怎样的？行为背后的动机是什么？ |
| L2 · 时代语境 | 故事所属的社会/历史背景 | 这个时代给人物施加了什么约束？什么力量在塑造他们的选择？ |
| L3 · 作者表达 | 真实作者 | 作者的个人经历如何映射进作品？TA 试图通过这个故事表达什么？ |

### 1.2 传播哲学：学术为底，通俗为面

这个项目的定位类似于**文学心理版的知乎**——底层有严谨的分析框架和原文证据链，但面向读者的表达是通俗、有网感、可分享的。

**为什么不走纯学术路线。** 学术论文的读者是同行，而这个项目的读者是普通文学爱好者。如果一份人物档案读起来像临床诊断报告，它会在传播的第一秒就失败了。我们的目标是让读者发出"原来是这样！"的感叹，然后转发给也在读这本书的朋友。

**通俗化的具体手段：**

- **定性分析使用故事化叙事。** 不是"该人物呈现出焦虑-矛盾型依恋模式"，而是"林黛玉紧紧抓住每一段关系，因为她从经验中学到——抓得不够紧的东西都会消失"。两者说的是同一件事，但后者读者能记住。
- **定量数据服务于直观对比。** "贾宝玉的神经质处于全体已分析人物的第 89 百分位"比"神经质得分 8.9"更有意义——因为它立刻在读者脑中建立了一个画面：这个人比绝大多数虚构人物都更情绪不稳定。
- **人物对比创造传播触点。** "贾宝玉 vs 拉斯柯尔尼科夫：两个被罪恶感吞噬的年轻人，一个选择了出家，一个选择了自首"——这种跨文化、跨作品的人物对话，是社交媒体上的天然内容。
- **免责声明要诚实但不扫兴。** 在页面底部标注"以上分析基于心理学框架对虚构人物的解读，仅供阅读辅助，不构成临床诊断"，而不是在每个结论前加"这只是一个可能的解释"——后者会杀死阅读体验。

### 1.3 核心原则

**可追溯。** 每一条心理推断都必须有原文引用支撑。读者应该能顺着链条走回到原文，自己判断分析是否合理。推断可以用不同的框架（精神分析、认知行为、依恋理论），但必须标注使用了哪种框架。

**渐进式披露。** 数据分析不能剧透。查询人物档案前必须询问读者进度，超出进度的内容折叠并标注警告。

**深而不广。** 每本书只做 3–8 个主要人物，但每个人物做透。不做 IMDb 式的标签罗列。

**开放贡献。** 任何人都可以提交新人物档案、修正分析、补充理论视角。贡献走审核流程，版本可追溯。

**中英双语。** 所有档案同步维护中文和英文两个版本（不是机翻，是独立撰写的两个语言版本）。中文面向知乎/小红书/豆瓣读者群，英文面向 Goodreads/Reddit/Substack 读者群。

---

## 二、数据结构

### 2.1 人物档案 (L1 · Character Profile)

每份档案是一个结构化 JSON 文档，存储在 `data/works/{work_id}/characters/{character_id}.json`。

```
顶层结构
├── meta                          # 元信息
├── identity                      # 身份层
├── profile                       # 心理画像层（定性+定量）
├── formative_events              # 创伤与关键经验
├── scene_annotations             # 行为注解（按章节索引，渐进披露）
├── arc                           # 人物弧光
├── layer2_linkages              # 链接到 L2 时代分析的相关条目
└── layer3_linkages              # 链接到 L3 作者表达的相关条目
```

#### meta（元信息）

```json
{
  "character_id": "lin-daiyu",
  "character_name": "林黛玉",
  "character_name_en": "Lin Daiyu",
  "aliases": ["颦儿", "潇湘妃子"],
  "aliases_en": ["Frowner", "Queen of the Bamboo"],
  "work_id": "hongloumeng",
  "work_title": "红楼梦",
  "work_title_en": "Dream of the Red Chamber",
  "author": "曹雪芹",
  "author_en": "Cao Xueqin",
  "author_nationality": "中国",
  "author_nationality_en": "China",
  "author_era": "清朝（约 1715–1763）",
  "author_era_en": "Qing Dynasty (c. 1715–1763)",
  "profile_version": "1.0.0",
  "last_updated": "2026-07-06",
  "contributors": [
    {"name": "AI 初稿", "role": "generator"},
    {"name": "张三", "role": "reviewer"}
  ],
  "confidence_level": "reviewed"
}
```

**双语字段说明：** 以 `_en` 结尾的字段为英文版本。中文和英文档案是两个独立的 Markdown/JSON 文件（`character.zh-CN.md` / `character.en.md`），使用相同的结构化字段但独立撰写——不是逐字段翻译，而是各自用目标语言的最佳表达来写。中文版可以引用中文译本原文，英文版引用英文译本原文。两个版本的心理学分析结论应当一致（同一套定量评分），但叙事风格和示例选择可以不同。

#### identity（身份层）

```json
{
  "age_range": "约 12–17 岁（书中时间跨度）",
  "gender": "女",
  "social_role": "贾母外孙女 / 寄居于贾府的贵族孤女",
  "social_class": "书香门第（父亲林如海为巡盐御史，已故）",
  "occupation": "无（闺阁女子）",
  "key_traits_summary": "敏感、聪慧、多愁善感、孤高、才华横溢、尖刻中藏着脆弱",
  "key_traits_summary_en": "hypersensitive, brilliant, melancholic, aloof, artistically gifted, sharp-tongued yet fragile",
  "relationship_graph": {
    "nodes": [
      {"id": "daiyu", "label": "林黛玉", "label_en": "Lin Daiyu", "weight": 1.0},
      {"id": "baoyu", "label": "贾宝玉", "label_en": "Jia Baoyu", "weight": 1.0},
      {"id": "baochai", "label": "薛宝钗", "label_en": "Xue Baochai", "weight": 0.9},
      {"id": "jiamu", "label": "贾母", "label_en": "Grandmother Jia", "weight": 0.7},
      {"id": "xifeng", "label": "王熙凤", "label_en": "Wang Xifeng", "weight": 0.5},
      {"id": "xiren", "label": "袭人", "label_en": "Xiren", "weight": 0.4},
      {"id": "zijuan", "label": "紫鹃", "label_en": "Zijuan", "weight": 0.4}
    ],
    "edges": [
      {"source": "daiyu", "target": "baoyu", "relation": "灵魂知己/未完成的爱情", "relation_en": "soulmate / unfulfilled love", "intensity": 1.0},
      {"source": "daiyu", "target": "baochai", "relation": "情感对手/隐秘的互相理解", "relation_en": "romantic rival / hidden mutual understanding", "intensity": 0.8},
      {"source": "daiyu", "target": "jiamu", "relation": "外祖母/依赖与疏远的张力", "relation_en": "maternal grandmother / tension between dependence and distance", "intensity": 0.6},
      {"source": "daiyu", "target": "zijuan", "relation": "贴身丫鬟/超越主仆的关怀", "relation_en": "maid / care beyond duty", "intensity": 0.5}
    ]
  }
}
```

#### profile（心理画像层）

```json
{
  "qualitative": {
    "personality_narrative": {
      "content": "林黛玉是一个高度敏感的灵魂被置于一个注定衰落的贵族家庭中。她的敏感不是矫情——是对环境威胁的精确雷达。父母双亡后，她在贾府这个'别人家'里没有任何制度性保障，唯一能依赖的只有贾母的疼爱和宝玉的感情——而这两样东西都不稳定。所以她的'小心眼'本质上是生存策略：对任何可能侵蚀这两样东西的信号保持最高级别的警觉。",
      "content_en": "Lin Daiyu is a hypersensitive soul placed inside a declining aristocratic family. Her sensitivity is not affectation — it's a precise radar for environmental threats. After losing both parents, she has no institutional security within the Jia household. The only things she can rely on are her grandmother's affection and Baoyu's love — and neither is stable. Her so-called 'petty temper' is fundamentally a survival strategy: maintaining maximum vigilance against any signal that might erode either of these two anchors.",
      "citations": [
        {"text": "黛玉便忖度着：因他有玉，故问我有也无。因答道：'我没有那个。想来那玉亦是一件罕物，岂能人人有的。'", "chapter": 3},
        {"text": "黛玉听了，不觉气怔在门外……自己又回思一番：'虽说是舅母家如同自己家一样，到底是客边。'", "chapter": 26}
      ],
      "framework": "依恋理论 / 创伤心理学"
    },
    "core_drives": {
      "primary_desire": "被坚定地选择——不是被可怜，不是被容忍，而是被毫无保留地放在第一位",
      "primary_desire_en": "To be firmly chosen — not pitied, not tolerated, but placed first without reservation",
      "primary_fear": "被抛弃、被替代、被遗忘",
      "primary_fear_en": "Abandonment, replacement, being forgotten",
      "internal_conflicts": [
        "渴望亲密 vs 害怕亲密（因为所有她亲密过的人都离开了）",
        "以才华维持自尊 vs 才华在闺阁制度中毫无价值",
        "对'金玉良缘'的不安 vs 对自己'草木之人'身份的悲哀"
      ],
      "internal_conflicts_en": [
        "Desire for intimacy vs fear of intimacy (everyone she's been close to has left)",
        "Self-worth anchored in literary talent vs talent being worthless in the women's quarters",
        "Anxiety about the 'Gold and Jade' prophecy vs grief over her own 'wood-and-plant' identity"
      ],
      "citations": [
        {"text": "黛玉道：'你死了，我做和尚去。'", "chapter": 30}
      ],
      "framework": "依恋理论 / 存在主义心理学"
    },
    "defense_mechanisms": [
      {
        "mechanism": "预先攻击",
        "mechanism_en": "Preemptive Strike",
        "description": "在预期到被冷落或伤害之前，先一步用尖刻言辞推开对方——'与其等你离开我，不如我先推开你'。这是遗弃创伤的经典防御模式。",
        "description_en": "Before anticipating coldness or hurt, she pushes people away with sharp words first — 'better I push you away than wait for you to leave me.' A classic defense pattern of abandonment trauma.",
        "citations": [
          {"text": "黛玉便说道：'我就知道，别人不挑剩下的也不给我。'", "chapter": 7}
        ],
        "framework": "精神分析 / 创伤心理学"
      },
      {
        "mechanism": "躯体化",
        "mechanism_en": "Somatization",
        "description": "心理痛苦转化为身体症状——咳嗽、失眠、食欲不振。在无法用语言表达愤怒和悲伤的环境中（闺阁女性的情绪表达被严格规训），身体成为唯一合法的抗议场所。",
        "description_en": "Psychological pain converted into physical symptoms — coughing, insomnia, loss of appetite. In an environment where anger and grief cannot be verbally expressed (women's emotional expression was strictly regulated in闺阁), the body becomes the only legitimate site of protest.",
        "citations": [
          {"text": "黛玉每岁至春分秋分之后，必犯嗽疾。", "chapter": 45}
        ],
        "framework": "身心医学 / 女性主义心理学"
      }
    ],
    "attachment_style": {
      "style": "焦虑-矛盾型依恋",
      "style_en": "Anxious-Ambivalent Attachment",
      "description": "童年丧母、少年丧父——两次依恋对象的丧失塑造了她对关系的基本预期：重要的人都会离开。她反复用争吵测试宝玉的感情，不是因为她不信任他，恰恰是因为她太需要他，以至于必须一遍遍确认他还在。",
      "description_en": "Losing her mother in childhood and father in adolescence — two attachment figure losses shaped her fundamental expectation: important people will leave. She repeatedly tests Baoyu's feelings through arguments, not because she distrusts him, but precisely because she needs him so much that she must verify his presence again and again.",
      "citations": [
        {"text": "黛玉听说，回手向书架上取下一本……指着宝玉道：'你这该死的胡说！好好儿的把这淫词艳曲弄了来……'", "chapter": 23}
      ],
      "framework": "依恋理论 (Bowlby/Ainsworth)"
    },
    "cognitive_patterns": [
      {
        "pattern": "命运化归因",
        "pattern_en": "Fatalistic Attribution",
        "description": "将伤害解读为命运的必然安排（'我命苦''草木之人'），而非具体的人际冲突。这种归因方式有两面性：一方面加深了无力感，另一方面提供了一种诗意的意义框架——'不是我不够好，是天意如此'——保护了核心自尊。",
        "description_en": "Interpreting pain as fate's inevitable arrangement rather than specific interpersonal conflicts. This attribution style is double-edged: it deepens helplessness while providing a poetic meaning framework — 'it's not that I'm not good enough, it's heaven's will' — which protects core self-esteem.",
        "citations": [
          {"text": "黛玉道：'我没这么大福禁受，比不得宝姑娘，什么金什么玉的，我们不过是草木之人。'", "chapter": 28}
        ],
        "framework": "认知行为理论 / 叙事心理学"
      }
    ],
    "moral_framework": {
      "description": "林黛玉的道德世界不是儒家伦理的，而是诗性正义的。她的'对错'不由社会规范定义，而由情感的真与假、关系中的忠诚与背叛来定义。这使得她在大观园的女性群体中既格格不入又极具道德魅力。",
      "description_en": "Daiyu's moral universe is not Confucian but poetically just. Her 'right and wrong' is defined not by social norms but by emotional authenticity vs falseness, loyalty vs betrayal in relationships. This makes her both out of place and morally compelling among the women of Prospect Garden.",
      "citations": [
        {"text": "黛玉道：'我也不要它。你也不必给我。'——对北静王所赠鹡鸰香串的反应", "chapter": 16}
      ],
      "framework": "道德心理学 / 情感伦理"
    }
  },
  "quantitative": {
    "big_five": {
      "openness": 9.0,
      "conscientiousness": 4.0,
      "extraversion": 2.5,
      "agreeableness": 3.5,
      "neuroticism": 9.5
    },
    "dark_triad": {
      "narcissism": 2.0,
      "machiavellianism": 2.0,
      "psychopathy": 1.0
    },
    "emotional_stability_index": 1.5,
    "cognitive_complexity": 9.0,
    "empathy_index": 8.0,
    "percentiles": {
      "neuroticism_percentile": 98,
      "openness_percentile": 95,
      "cognitive_complexity_percentile": 95,
      "emotional_stability_percentile": 1,
      "extraversion_percentile": 8
    }
  }
}
```

关键：定量评分需要锚定在一个**全体已分析人物的分布**上。百分位比绝对分数更有意义。"哈姆雷特的神经质处于全体人物的第 95 百分位"——这既是定性判断的量化表达，又为跨作品对比提供了基础。

#### formative_events（创伤与关键经验）

```json
[
  {
    "event_id": "fe-001",
    "timeline_order": 1,
    "event": "母亲贾敏早逝",
    "event_en": "Mother (Jia Min) dies in Daiyu's early childhood",
    "age_at_event": "约 6 岁",
    "description": "黛玉的母亲贾敏在她幼年时去世。这是黛玉生命中第一次依恋断裂。贾敏是贾母最疼爱的女儿，黛玉从母亲那里继承了进入贾府的'资格'，却失去了享受这份资格所必需的情感基础。",
    "description_en": "Daiyu's mother died when she was about six — the first attachment rupture of her life. Jia Min was Grandmother Jia's most beloved daughter, and through her Daiyu inherited the 'qualification' to enter the Jia household, while losing the emotional foundation needed to enjoy it.",
    "psychological_impact": "母亲的去世是黛玉被送入贾府的前提条件。她的每一次'寄人篱下'的刺痛感，根源都在这里：她是作为一个没有了母亲的孩子才来到这里，而这里最不缺的就是有母亲的孩子。",
    "citations": [
      {"text": "那女学生黛玉，身体方愈，原不忍弃父而往；无奈他外祖母致意务去……", "chapter": 3}
    ],
    "theoretical_basis": "依恋理论 (Bowlby)、童年丧亲研究",
    "manifestations_in_behavior": [
      "对'母亲意象'的矛盾需求（渴望贾母的疼爱但始终觉得不够）",
      "对宝钗拥有'完整的家庭背景'的隐性嫉妒"
    ]
  },
  {
    "event_id": "fe-002",
    "timeline_order": 2,
    "event": "父亲林如海去世",
    "event_en": "Father (Lin Ruhai) dies",
    "age_at_event": "约 10–11 岁",
    "description": "黛玉回家侍疾后，父亲林如海病故。至此，黛玉失去所有直系亲属，彻底成为'寄人篱下'的孤女。",
    "description_en": "After returning home to care for her ailing father, Lin Ruhai passes away. At this point, Daiyu has lost all immediate family members and becomes a complete orphan living under another family's roof.",
    "psychological_impact": "父亲的去世将黛玉从'暂时寄居'推入'无处可归'的状态。大观园从此不是她暂住的地方，而是她唯一能去的地方。这种'没有退路'的处境使她对关系的安全感极度敏感——每一段关系都是'最后的防线'。",
    "citations": [
      {"text": "谁知这年冬底，林如海的书信寄来，却为身染重疾，写书特来接林黛玉回去。", "chapter": 12}
    ],
    "theoretical_basis": "复杂哀伤理论、遗弃创伤 (abandonment trauma)",
    "manifestations_in_behavior": [
      "对宝玉与宝钗互动的过度警觉 → 见行为注解",
      "将'被选'还是'不被选'视为存在性问题 → 见人物弧光"
    ]
  }
]
```

#### scene_annotations（行为注解——渐进披露核心）

```json
[
  {
    "chapter": 27,
    "chapter_title_hidden": false,
    "spoiler_level": "none",
    "scene_summary": "黛玉葬花。她将落花收集、埋葬，吟诵《葬花吟》。",
    "scene_summary_en": "Daiyu buries fallen flowers and recites the 'Flower Burial Song.'",
    "emotions_observed": ["悲伤", "孤独", "诗意化的自我哀悼", "对自己命运的清醒预知"],
    "behaviors_observed": [
      "收集落花并埋葬",
      "吟诵长篇诗歌，以花自喻",
      "被宝玉撞见后最初回避，后对话"
    ],
    "psychological_explanation": "葬花行为不是简单的伤春悲秋。它是黛玉对自身处境的一次高度隐喻化的处理：(1) 前置性哀悼——她在自己还活着的时候就提前哀悼自己的死亡，这是一种心理防御，把'被遗忘的恐惧'转化为'我已经接受了这个结局'的叙事控制感；(2) 类比思维——她把落花和自己画等号：都是美好的、都是短暂的、都是没人真正在乎的、都是最终'质本洁来还洁去'的。这不是自我怜悯，是她在给自己的命运下定义——在一个她无法控制的处境中，至少'如何理解自己的命运'这件事由她自己说了算。",
    "psychological_explanation_en": "The flower burial is not mere sentimentality. It is Daiyu processing her situation through metaphor: (1) Anticipatory mourning — she mourns her own death while still alive, a psychological defense that transforms 'fear of being forgotten' into narrative control; (2) Analogical thinking — she equates fallen flowers with herself: beautiful, fleeting, uncared for, and ultimately returning to purity. This is not self-pity; it's her defining her own fate. In a situation she cannot control, at least how she *understands* her fate remains hers alone.",
    "linked_formative_events": ["fe-001", "fe-002"],
    "linked_era_analysis": ["era-qing-women-status-001"],
    "linked_author_analysis": ["author-cao-family-decline-001"],
    "citations": [
      {"text": "花谢花飞飞满天，红消香断有谁怜……一朝春尽红颜老，花落人亡两不知！", "chapter": 27}
    ],
    "alternative_interpretations": [
      {
        "framework": "社会心理学",
        "interpretation": "葬花也是一种表演性的身份宣示。在大观园中，每个女性都在以不同方式争取注意力——宝钗用德性、凤姐用权力、湘云用豪爽。黛玉的武器是诗性敏感。葬花是她最成功的'自我品牌展示'，在那一刻她不需要和任何人比较——她定义了什么是有价值的。"
      }
    ]
  },
  {
    "chapter": 45,
    "chapter_title_hidden": false,
    "spoiler_level": "minor",
    "scene_summary": "黛玉与宝钗冰释前嫌。宝钗探望病中的黛玉，建议用燕窝调养，黛玉倾诉了多年寄居的苦楚。",
    "scene_summary_en": "Daiyu and Baochai reconcile. Baochai visits the ill Daiyu and suggests bird's nest soup; Daiyu confides years of pain living as a dependent.",
    "emotions_observed": ["感激", "羞愧", "释然", "脆弱"],
    "behaviors_observed": [
      "向宝钗坦白多年误会",
      "承认自己'多心'",
      "接受宝钗的帮助（燕窝）"
    ],
    "psychological_explanation": "这是黛玉全书中最坦诚的心理暴露时刻。她对宝钗的敌意一直是'防御性的'——宝钗代表了她最恐惧的东西（被替代）。但当宝钗以关怀而非竞争的方式接近她时，黛玉的防御体系出现了裂缝。她说'往日竟是我错了'——这不是自贬，而是严重的心理突破：一个习惯于用攻击保护自己的人，允许自己在另一个人面前卸下武装。接受燕窝是一个强大的象征行为——她第一次接受了贾府中有人可以不伤害她。",
    "linked_formative_events": ["fe-001", "fe-002"],
    "linked_era_analysis": ["era-qing-women-friendship-001"],
    "citations": [
      {"text": "黛玉叹道：'你素日待人，固然是极好的，然我最是个多心的人，只当你心里藏奸。'", "chapter": 45}
    ],
    "alternative_interpretations": [
      {
        "framework": "叙事心理学",
        "interpretation": "这个和解场景的悲剧性在于它来得太晚了——或者说，它出现在一个无论如何都无法改变黛玉命运的叙事结构中。宝钗的关怀是真心的，但这种真心反而加深了'金玉良缘'叙事的残忍性：她不是坏人，可她还是会'赢'。"
      }
    ]
  }
]
```

spoiler_level 取值：`"none"`（无剧透，该场景不涉及关键剧情转折）、`"minor"`（次要剧透）、`"major"`（重大剧透）。配合用户的阅读进度，前端决定是否展示该条目。

#### arc（人物弧光）

```json
{
  "type": "tragic_descent",
  "opening_state": {
    "chapter": 3,
    "description": "初入贾府，年幼丧母，敏感而谨慎——'步步留心，时时在意，不肯轻易多说一句话，多行一步路'",
    "key_traits": ["谨慎", "敏感", "聪慧", "孤独"]
  },
  "turning_points": [
    {
      "chapter": 27,
      "spoiler_level": "minor",
      "event": "葬花——确立'以诗为命'的自我认同",
      "psychological_shift": "从被动承受命运转为主动为命运赋义。葬花之后，黛玉找到了自己在大观园中的精神位置：以诗歌和敏感为武器，在一个物质至上的世界里捍卫情感的纯度。"
    },
    {
      "chapter": 45,
      "spoiler_level": "minor",
      "event": "与宝钗和解——首次突破防御性人格",
      "psychological_shift": "承认了自己的'多心'是一种误解，接受了来自同性的关怀。这是全书中最温和的黛玉——她证明了自己有能力信任和接受爱，只是很少有人能走到这一步。"
    }
  ],
  "closing_state": {
    "chapter": 97,
    "spoiler_level": "major",
    "description": "在宝玉与宝钗成婚的同时焚稿断痴情，咯血而亡",
    "key_traits": ["绝望", "决绝", "以毁灭维护尊严"]
  },
  "arc_analysis": "林黛玉的弧光不是从弱到强或从强到弱的简单曲线。她自始至终都是敏感的——改变的是她处理敏感的方式。初期的敏感表现为对外界的小心翼翼；中期通过诗歌和爱情找到了将敏感转化为创造力的出口；后期在确认自己不被选择时，将敏感燃烧为一场彻底的自我毁灭。烧掉诗稿不是崩溃——是她最后的宣言：这些情感是我的，既然你不选择承载它们的人，那我也不让它们留在这个世界上被糟蹋。",
  "arc_analysis_en": "Daiyu's arc is not a simple curve from weak to strong or vice versa. She is sensitive throughout — what changes is how she handles it. In the beginning, sensitivity manifests as caution toward the outside world. In the middle, through poetry and love, she transforms it into creativity. In the end, when she confirms she has not been chosen, she burns sensitivity into total self-destruction. Burning her poetry manuscripts is not a breakdown — it is her final declaration: these feelings are mine, and since you didn't choose the person who carries them, I won't let them remain in this world to be trampled.",
  "framework": "叙事心理学 (McAdams) / 创伤与韧性研究"
}
```

### 2.2 时代语境分析 (L2 · Era Context)

存储在 `data/works/{work_id}/era/{era_id}.json`。

```
顶层结构
├── meta                          # 元信息
├── overview                      # 时代概览
├── social_structure              # 社会结构
├── norms_and_constraints         # 规范与约束
├── historical_events             # 关键历史事件
├── character_linkages           # 链接到具体人物：时代如何塑造了这个角色
├── further_reading              # 延伸阅读
└── citations                    # 全局引用来源
```

示例核心字段（以红楼梦的清代背景为例）：

```json
{
  "meta": {
    "era_id": "qing-dynasty-kangxi-qianlong",
    "era_name": "清朝康乾盛世",
    "era_name_en": "Qing Dynasty — Kangxi-Qianlong Flourishing Age",
    "time_range": "约 1680–1790（故事设定）/ 约 1740–1760（曹雪芹创作期）",
    "geography": "中国 / 帝都（北京）",
    "geography_en": "China / Imperial Capital (Beijing)",
    "work_id": "hongloumeng"
  },
  "overview": {
    "summary": "《红楼梦》的故事设定跨越贾府从盛到衰的数十年，背景融合了康熙、雍正、乾隆三朝的社会风貌。这是一个表面繁华、内里腐朽的时代：商品经济高度发达，但社会等级制度森严；科举仍是唯一的上升通道，但买官鬻爵已成公开秘密；女性的社会地位在理学规范的约束下被严格限制在家庭内部，但同时上层阶级的女性通过文学和艺术获得了有限但真实的精神空间。",
    "summary_en": "Dream of the Red Chamber spans decades of the Jia family's decline, set against the Kangxi, Yongzheng, and Qianlong reigns. This was an era of surface prosperity and internal decay: the commercial economy flourished, but the social hierarchy was rigid; the imperial examination remained the only upward channel, yet bribery for offices was an open secret; women's status was strictly confined to the domestic sphere under Neo-Confucian norms, though upper-class women gained limited but real spiritual space through literature and art.",
    "relevance_to_work": "贾府的兴衰不是个案——它是康乾盛世末期整个八旗贵族制度性衰败的缩影。理解大观园中每一个女性的命运，都需要先理解她们生活在一个'不嫁人就没有社会存在，嫁了人就失去精神存在'的制度中。"
  },
  "social_structure": {
    "class_system": "清代社会以旗民分治为基础，八旗贵族享有特权但被禁止从事商业和农业生产，依靠朝廷俸禄和地租生活。贾府作为包衣（满洲贵族的世袭家奴）出身、后因军功和联姻升入贵族阶层的家族，其经济来源高度依赖朝廷恩宠——这种制度性依赖是贾府衰败的结构性原因。",
    "class_system_en": "Qing society was divided between the Eight Banners nobility and commoners. Banner nobles enjoyed privileges but were forbidden from commerce or agriculture, relying on imperial stipends and land rents. The Jia family, originating as bondservants elevated through military merit and marriage, depended heavily on imperial favor — this institutional dependency structurally guaranteed their eventual decline.",
    "gender_roles": {
      "description": "清代上层女性受三重约束：礼教（'三从四德'）、法律（无独立财产权、无婚姻自主权）和家族政治（婚姻是家族联盟的工具）。大观园表面上是少女的天堂，实际上是婚姻市场到来前的临时庇护所——每个女孩都知道，离开大观园的那一天，就是自由终结的那一天。",
      "description_en": "Upper-class Qing women were constrained by three forces: Neo-Confucian ritual ('Three Obediences and Four Virtues'), law (no independent property rights, no marriage autonomy), and family politics (marriage as an instrument of alliance). Prospect Garden was superficially a paradise for girls — in reality it was a temporary shelter before the marriage market arrived. Every girl knew: the day she leaves the Garden is the day her freedom ends."
    },
    "marriage_and_family": {
      "description": "贵族婚姻由父母和家族利益决定。'金玉良缘'（宝钗的金锁与宝玉的通灵玉）本质上是一场精心安排的家族联盟，而'木石前盟'（黛玉的前世绛珠仙草与宝玉的前世神瑛侍者）则是个人情感的隐喻。这场三角关系的残酷之处在于：每个人的选择都不是自己做的，但每个人都要为自己的'选择'承受后果。",
      "description_en": "Aristocratic marriages were decided by parents and family interests. The 'Gold and Jade' match was essentially a calculated family alliance, while the 'Wood and Stone' bond was a metaphor for personal feeling. The cruelty of this triangle: nobody made their own choice, yet everyone bore the consequences of the 'choice' made for them."
    },
    "religion_worldview": "《红楼梦》融合了儒释道三家——儒家（家族责任和礼教秩序，但书中对其持批判态度）、佛家（一切皆空、繁华终归虚幻，这是全书的结构性主题）、道家（自然、逍遥、反礼教，宝玉的精神归宿）。三家不是并列的，而是书中人物在不同人生阶段的精神锚点：贾政是儒家、宝玉是道家、惜春是佛家——每个人都在用不同的世界观消化家族的衰败。"
  },
  "norms_and_constraints": [
    {
      "norm": "闺阁制度与女性才德观",
      "norm_en": "The Inner Quarters System and 'Talent vs Virtue' View of Women",
      "description": "清代主流观念认为'女子无才便是德'。林黛玉和薛宝钗的才华在制度上没有价值——她们的诗歌再好，也不会有人为此给她们自由。但《红楼梦》本身就是在反抗这种观念：书中女性角色的才华被曹雪芹用工笔描绘、郑重对待，她们的诗会被抄录、品评、传阅——在大观园内部，文学为女性提供了一种替代性的社会评价体系。",
      "character_impacts": [
        {
          "character_id": "lin-daiyu",
          "impact": "黛玉的自我价值感高度依赖诗歌才华，因为这是她在闺阁制度内唯一能获得认可的维度。但她同时清醒地知道这种认可的边界——诗歌写得好不能改变她作为孤女在婚姻市场上的劣势。这种'才华是唯一的，但唯一的没有用'的困境，是她持续痛苦的结构性来源之一。"
        }
      ]
    }
  ],
  "historical_events": [
    {
      "event": "曹家由盛转衰：江宁织造曹頫被抄家（1728年）",
      "event_en": "The Cao family's fall: Imperial Textile Commissioner Cao Fu's household was confiscated (1728)",
      "date": "1728",
      "relevance": "曹雪芹家族在雍正年间被抄家，从钟鸣鼎食跌入贫寒。《红楼梦》中贾府的抄家是这部家族史的艺术化再现。这不是影射——是曹雪芹把自己经历过的事情拆解、重组、放大，让贾府成为所有类似家族命运的寓言。"
    }
  ]
}
```

### 2.3 作者表达分析 (L3 · Author Expression)

存储在 `data/works/{work_id}/author.json`。

这是整个框架中最微妙的一层。我们不声称"作者就是想表达这个"——我们呈现作者的生平事实、时代经历、其他作品中的主题线索，然后建立与当前作品的**映射**，让读者自己判断。

```
顶层结构
├── meta                          # 元信息
├── biography                     # 关键生平事件（与作品创作时间重叠的部分重点标注）
├── thematic_preoccupations       # 作者反复关注的主题（跨作品分析）
├── work_mappings                 # 生平事件 → 作品元素的映射
├── expressive_drive_analysis     # 表达欲望分析
├── other_works_citations        # 引自作者其他作品/信件/日记的证据
└── alternative_readings          # 替代解读
```

核心字段（以曹雪芹为例）：

```json
{
  "meta": {
    "author_name": "曹雪芹",
    "author_name_en": "Cao Xueqin",
    "birth_death": "约 1715 – 约 1763",
    "work_id": "hongloumeng",
    "work_creation_period": "约 1740 – 1763（未完成，前八十回）"
  },
  "biography": {
    "timeline": [
      {
        "date": "约 1715",
        "event": "出生于江宁织造曹家，曾祖父曹玺、祖父曹寅、父辈曹颙/曹頫三代四人担任江宁织造近六十年",
        "age_of_author": 0,
        "relevance_note": "曹家的江宁织造身份是《红楼梦》中贾府富贵生活的直接素材。贾府不是虚构的——它是曹雪芹亲身经历过的奢华生活的艺术化再造。"
      },
      {
        "date": "1728",
        "event": "曹家被雍正帝下令抄家，家族由南京迁回北京，从此衰败",
        "age_of_author": 13,
        "relevance_note": "抄家是曹雪芹一生中最重要的创伤事件。他在十三岁时从钟鸣鼎食跌入贫寒——《红楼梦》中贾府的抄家、宝玉最终的落魄，都是这场个人灾难的文学转化。十三岁是一个关键年龄：足够大到记住繁华的每一个细节，足够小到无法做任何事阻止它。"
      },
      {
        "date": "约 1740–1763",
        "event": "在北京西山贫病交加中创作《红楼梦》。幼子夭折后悲痛过度，不久去世。",
        "age_of_author": "25–48",
        "relevance_note": "曹雪芹在贫困中创作了这部关于富贵的小说——这种反差本身就是理解全书的关键。他写下每一个关于锦衣玉食、诗词雅集、家族宴饮的细节时，都带着'这一切我已经失去了'的双重视角：既是亲历者，也是悼念者。"
      }
    ],
    "key_losses_during_writing": [
      "家族被抄没（13岁）——从贵族子弟沦为贫民",
      "幼子夭折（晚年）——据传此事件直接加速了曹雪芹的去世"
    ]
  },
  "thematic_preoccupations": [
    {
      "theme": "繁华与衰败的必然性",
      "theme_en": "The inevitability of prosperity and decline",
      "across_works": ["红楼梦（全书）"],
      "interpretation": "曹雪芹在《红楼梦》开篇就借一僧一道之口说'那红尘中有却有些乐事，但不能永远依恃'。他不是在写一个家族的偶然衰败——他在写所有家族的必然衰败。这种'先告诉你结局，再让你看过程'的叙事策略，本质上是一种哀悼的仪式：他知道结局会怎样，所以他在结局到来之前，把每一个细节都郑重地记下来。"
    },
    {
      "theme": "男性中心叙事的解构",
      "theme_en": "Deconstructing male-centered narrative",
      "across_works": ["红楼梦（全书）"],
      "interpretation": "曹雪芹在开篇自述中说'我之罪固不免，然闺阁中本自历历有人，万不可因我之不肖，自护己短，一并使其泯灭也'。这在整个中国古典小说传统中是独一无二的——一个男性作者，在自传性质的小说中明确将叙事的合法性建立在'为女性立传'之上。贾宝玉的'女儿是水做的骨肉，男人是泥做的骨肉'不只是一个公子哥的怪癖——它是曹雪芹本人对男性中心的权力结构（包括他自己作为男性受益者的身份）的反思和忏悔。"
    }
  ],
  "work_mappings": [
    {
      "biographical_event": "曹家被抄家（1728）",
      "work_element": "贾府被抄家",
      "mapping_type": "biographical_parallel",
      "analysis": "贾府的抄家不是曹家的简单复制——它是曹雪芹将个人记忆与普遍命运主题结合的产物。书中抄家的原因（贾赦、贾珍的罪行）与历史上曹家被抄的原因（政治失宠而非具体罪行）不完全一致——曹雪芹将政治悲剧'道德化'了，使之成为因果报应叙事的一部分。这是小说家对个人创伤的重组和赋义。",
      "confidence": "scholarly_consensus"
    },
    {
      "biographical_event": "从富贵到贫困的个人经历",
      "work_element": "整部小说的双重叙事视角——繁华与凋零同时存在于叙事者的眼中",
      "mapping_type": "thematic_echo",
      "analysis": "《红楼梦》最惊人的艺术成就是它的叙事者——一个同时知道开头和结尾的人。他知道大观园的诗会不会永远开下去，知道每一个笑声最终都会变成哭声。这种'预先哀悼'的视角，来自曹雪芹本人的生活经验：他在写富贵的时候已经一贫如洗，所以他知道每一件绫罗绸缎最终都会变卖，每一顿山珍海味最终都会变成'举家食粥酒常赊'。",
      "confidence": "scholarly_consensus"
    }
  ],
  "expressive_drive_analysis": {
    "summary": "曹雪芹用《红楼梦》做了三件事。第一，悼念：悼念他失去的家族、失去的童年、失去的女性亲友——他在开篇明确说'以告天下人：我之负罪固多，然闺阁中历历有人，万不可因我之不肖，一并使其泯灭也'。第二，忏悔：作为一个富贵家族的男性后代，他享受了制度给予的一切特权，也见证了这些特权如何摧毁了周围的女性和他自己。第三，反抗：在'女子无才便是德'的时代，他用一部百万字的小说为女性的才华、情感和命运立了一座纪念碑。",
    "summary_en": "Cao Xueqin did three things with Dream of the Red Chamber. First, mourning: he mourned his lost family, lost childhood, and lost female relatives — he explicitly states in the opening: 'the women in the inner quarters are worthy of record, and I cannot let them be forgotten just because of my own failings.' Second, confession: as a male descendant of a wealthy family, he enjoyed every privilege the system offered and witnessed how those privileges destroyed the women around him and himself. Third, rebellion: in an era when 'women's talentlessness is virtue,' he used a million-word novel to build a monument to women's talent, emotion, and fate.",
    "core_questions_the_author_seems_to_be_asking": [
      "一个繁荣的家族为什么注定要衰败？",
      "在一个不承认女性主体性的社会里，女性的情感和才华如何被看见、被记住？",
      "如果一切繁华最终都会化为尘土，人在活着的时候该如何自处？"
    ]
  },
  "alternative_readings": [
    {
      "school": "马克思主义批评",
      "school_en": "Marxist criticism",
      "reading": "贾府的衰败本质上是封建贵族经济的结构性崩溃——依靠地租和朝廷俸禄的经济基础无法支撑越来越庞大的寄生性消费。《红楼梦》是封建制度自我瓦解的文学化呈现。"
    },
    {
      "school": "佛教/存在主义视角",
      "school_en": "Buddhist/existentialist perspective",
      "reading": "《红楼梦》的核心不是社会批判，而是存在性的——'好便是了，了便是好'。所有的社会分析、人物心理学，最终都服务于一个更根本的问题：在一个一切最终都会消失的世界里，活着本身是否有意义？"
    }
  ]
}
```

### 2.4 三层之间的链接机制

L1 和 L2、L3 之间通过双向链接关联：

- L1 的 `layer2_linkages` 指向相关的时代分析条目
- L1 的 `layer3_linkages` 指向相关的作者分析条目
- L2 的 `character_impacts` 指向受该社会规范影响的人物
- L3 的 `work_mappings` 指向映射到的作品元素

前端渲染时，人物档案页面的侧边栏可以显示"这个行为在当时的社会规范下意味着什么 →"和"作者本人经历过类似的事 →"的链接，让读者可以在三层之间自由跳转。

---

## 三、渐进式披露设计

### 3.1 用户进度模型

```
用户状态 = {
  work_id: "hamlet-1603",
  chapter: 3,
  scene: 1,
  chapter_title_known: "第三幕 第一场"  // 用户可以只标到章，不标到节
}
```

### 3.2 披露规则

| 档案内容 | 披露策略 |
|---------|---------|
| meta | 始终可见 |
| identity | 始终可见 |
| profile (定性 + 定量) | 始终可见（不涉及剧情细节） |
| formative_events | 仅披露 `timeline_order` 对应章节 ≤ 用户进度的条目；超出部分折叠，标注"以下内容可能包含剧透" |
| scene_annotations | 仅披露 `chapter` ≤ 用户进度的条目（scene 也需 ≤ 用户进度） |
| arc | `opening_state` 始终可见；`turning_points` 和 `closing_state` 按章节进度披露 |
| layer2 / layer3 | 始终可见（时代和作者分析不直接剧透情节） |

### 3.3 入口交互

进入任何一个人物档案页时：

1. 检测 localStorage 是否已有该作品的阅读进度
2. 如无，弹出进度设置对话框："你读到了第几章？"（可跳过）
3. 用户设置进度后，页面按披露规则渲染
4. 页面顶部常驻进度指示器，用户可以随时调整
5. 被折叠的内容显示模糊遮罩 + "以下内容可能包含剧透，点击查看（将记录你的进度）"

---

## 四、生成流水线

### 4.1 总览

```
源材料准备 → 人物识别 → L1 逐层生成 → L2 时代分析 → L3 作者分析
    ↓
定性审校 → 定量校准 → 分层随机抽检 → 问题族追杀 → 归档发布
```

### 4.2 各阶段详情

**阶段零：源材料准备。** 获取作品全文（公版书从 Project Gutenberg / 中文公版书源获取），确定章节分界，生成本文索引。如果作品仍在版权期，仅存储章节号索引和短引用（不超过合理使用范围），不存储全文。

**阶段一：人物识别。** AI 通读全文，输出人物清单，标注叙事权重（出场频次 × 情节重要性 × 是否有独立 POV）。人工（或 AI reviewer）复核，选定 3–8 个主要人物。同步产出初步的关系图谱。

**阶段二：L1 逐层生成。** 对每个主要人物，按 schema 逐层分析。每一层是独立的 AI 任务，有独立的 prompt 模板和质量检查清单。关键约束：
- 每一条心理推断必须附带原文引用
- 每个场景注解必须标注使用的心理学框架
- 定量评分必须在同一作品的已分析人物之间做相对排序（不引入外部参照导致评分失锚）

**阶段三：L2 时代分析。** 基于作品创作年代和故事背景年代，生成时代语境档案。这一层需要外部史料支撑——AI 可能产生"合理但虚构的历史细节"，所以必须要求 AI 区分"有史料来源的断言"和"基于时代背景的合理推测"，并标注信息来源。

**阶段四：L3 作者分析。** 整合作者传记资料、书信/日记、其他作品中的主题线索，建立生平→作品映射。映射必须有类型标签（`biographical_parallel` / `thematic_echo` / `speculative` / `scholarly_consensus`）和置信度。

**阶段五：定性审校。** 人类审查者检查：
- 心理推断是否过度解读？
- 原文引用是否支撑结论？
- 理论框架使用是否恰当？
- 有没有遗漏关键场景？
- 跨层链接是否合理？

**阶段六：定量校准。** 检查同一评分者的内部一致性（类似人物是否给了类似分数），确保百分位锚定在全体已分析人物分布上。

**阶段七：分层随机抽检与问题族追杀。** 借鉴 LifeBook 的方法。抽检发现一个类型问题，不在该样本上修完就结束，而是：
1. 归纳问题族（"把角色的讽刺误读为真诚"）
2. 全书同类审计（搜遍所有人物档案中的相关场景）
3. 系统性修复
4. 记录例外
5. 用新 seed 追加新一轮抽检

**阶段八：归档发布。** 生成带版本号的档案文件，部署到网站。

---

## 五、技术方案

### 5.1 技术选型

| 层 | 选择 | 理由 |
|---|------|------|
| 框架 | Next.js (App Router) | React 生态、SSG/SSR 灵活、部署零配置 |
| 样式 | Tailwind CSS + 自定义设计 token | 快速开发、视觉一致性 |
| 图表 | Chart.js（雷达图、散点图）+ Mermaid（关系图谱） | 轻量、文档好 |
| 内容存储 | Git 仓库中的 JSON/Markdown 文件 | 版本可追溯、PR 流程天然适合贡献、无需数据库运维 |
| 用户数据 | localStorage（阅读进度） | 无需后端、隐私友好 |
| 贡献系统 | GitHub PR → 审核 → 合并 → 自动部署 | 零成本、成熟的协作流程 |
| 部署 | Vercel (Hobby 计划) | 免费、Git 集成、自动部署 |
| AI 生成 | Claude API / OpenAI API（生成阶段使用，不耦合到生产代码） | 生成是一次性的，不需要在网站中集成 AI |

### 5.2 项目结构

```
life-in-book/
├── public/                        # 静态资源
│   └── images/                    # 作者肖像、作品封面等
├── src/
│   ├── app/                       # Next.js App Router
│   │   ├── layout.tsx
│   │   ├── page.tsx               # 首页（作品列表 + 项目介绍）
│   │   ├── works/
│   │   │   └── [work_id]/
│   │   │       ├── page.tsx       # 作品主页（三层入口）
│   │   │       ├── characters/
│   │   │       │   └── [character_id]/page.tsx  # 人物档案页
│   │   │       ├── era/page.tsx   # 时代分析页
│   │   │       └── author/page.tsx # 作者分析页
│   │   ├── compare/page.tsx       # 人物对比页
│   │   ├── explore/page.tsx       # 排行榜/探索页
│   │   ├── contribute/page.tsx    # 贡献指南
│   │   └── [locale]/              # 语言路由 (zh / en)
│   ├── components/                # 复用组件
│   │   ├── ProgressGate.tsx       # 进度门禁
│   │   ├── RadarChart.tsx         # 雷达图
│   │   ├── RelationshipGraph.tsx  # 关系图谱
│   │   ├── SpoilerBlur.tsx        # 剧透模糊遮罩
│   │   ├── CitationBlock.tsx      # 原文引用块
│   │   ├── CharacterCard.tsx      # 人物卡片
│   │   ├── PercentileBadge.tsx    # 百分位标签
│   │   ├── LanguageToggle.tsx     # 中英切换
│   │   └── LayerLinkage.tsx       # 跨层链接
│   ├── lib/
│   │   ├── data.ts                # 数据加载（读取 JSON/Markdown）
│   │   ├── progress.ts            # 阅读进度管理
│   │   ├── spoiler-filter.ts      # 剧透过滤逻辑
│   │   └── i18n.ts                # 国际化工具
│   └── types/                     # TypeScript 类型定义
├── data/                          # 内容仓库（核心）
│   └── works/
│       └── {work_id}/
│           ├── work.json           # 作品元信息（双语字段在同一 JSON 中）
│           ├── characters/
│           │   └── {character_id}/
│           │       ├── profile.zh-CN.md  # 中文人物档案
│           │       └── profile.en.md     # 英文人物档案
│           ├── era/
│           │   └── {era_id}/
│           │       ├── era.zh-CN.md
│           │       └── era.en.md
│           └── author/
│                ├── author.zh-CN.md
│                └── author.en.md
├── prompts/                       # AI 生成用的 prompt 模板
│   ├── character_identification.md
│   ├── l1_profile.zh-CN.md
│   ├── l1_profile.en.md
│   ├── l1_annotations.zh-CN.md
│   ├── l2_era.zh-CN.md
│   ├── l2_era.en.md
│   ├── l3_author.zh-CN.md
│   ├── l3_author.en.md
│   └── quality_review.md
├── docs/                          # 项目文档
│   ├── CONTRIBUTING.zh-CN.md
│   ├── CONTRIBUTING.en.md
│   ├── SCHEMA.md                  # 数据结构规范
│   └── REVIEW_GUIDE.md            # 审校指南
├── tailwind.config.ts
├── next.config.ts
├── package.json
└── tsconfig.json
```

### 5.3 关键组件设计

**ProgressGate。** 一个 React Context Provider，管理用户的阅读进度状态。读取 localStorage 中的进度数据，提供 `setProgress(workId, chapter, scene)` 和 `isSpoiler(workId, chapter, scene)` 方法。

**SpoilerBlur。** 包裹被折叠的剧透内容，显示模糊遮罩 + 警告文字。点击后更新用户进度（询问确认），然后展示内容。支持两种模式：`blur`（模糊化）和 `hidden`（完全隐藏，用于重大剧透如结局）。

**ProgressPrompt。** 进入人物档案页时，如果 `progress[workId]` 不存在，弹出进度设置对话框。显示章节列表（从 `work.json` 中读取），用户可单选一章或点击"我还没开始读"。

**RadarChart。** 包装 Chart.js 的雷达图组件，展示大五人格或可选的其他维度。同时显示该人物在全体人物库中的百分位标签。

**RelationshipGraph。** 使用 Mermaid 或 D3 渲染人物关系图谱，节点按权重缩放，边的样式表示关系类型（爱/恨/血缘/权力）。

### 5.4 数据加载策略

采用 Next.js 的静态生成（SSG）。`data/` 目录下的 JSON 文件在构建时被读取，生成静态页面。这意味着：

- 添加新人物档案 = 添加 JSON 文件 + 提交 PR + 合并 → Vercel 自动重新部署
- 页面加载极快（纯静态 HTML）
- 不需要数据库，不需要服务器
- 贡献者只需要会写 JSON（或用我们提供的生成工具）

未来如果数据量增长到数千份档案，可以迁移到内容管理系统（如 Sanity 或 Strapi），但 MVP 阶段不需要这个复杂度。

---

## 六、开放贡献体系

### 6.1 贡献类型

| 类型 | 所需技能 | 示例 |
|------|---------|------|
| 提名作品 | 无 | "建议分析《百年孤独》的布恩迪亚家族" |
| 补充引用 | 读过该书 | "哈姆雷特在第 X 幕第 Y 场还说过……，可以补充到防御机制分析中" |
| 修正分析 | 心理学/文学背景 | "把奥菲利亚的'suicide'改为'ambiguous death'更准确" |
| 提交新档案 | 能操作 JSON + AI | 完整的人物/时代/作者档案 |
| 新增理论框架 | 心理学专业 | "建议增加'复杂性哀伤理论'作为创伤分析框架" |
| 代码贡献 | 开发 | 改进网站功能、新增可视化组件 |
| 翻译档案 | 多语言能力 | 将中文档案翻译为英文版 |

### 6.2 贡献流程

```
Fork 仓库 → 创建分支 → 按模板编写/修改 JSON
    ↓
提交 PR（附带 checklist）
    ↓
自动检查：
  - JSON schema 校验
  - 引用完整性检查（citation 的章节是否存在于 work.json 中）
  - Lint 通过
    ↓
人工审核：
  - 心理推断是否有原文支撑
  - 理论框架使用是否恰当
  - 置信度标签是否合适
    ↓
合并 → Vercel 自动部署
```

### 6.3 外部 API

提供简单的 REST API 供外部服务调用：

```
GET /api/works                          # 作品列表
GET /api/works/{work_id}                # 作品详情
GET /api/works/{work_id}/characters     # 人物列表
GET /api/works/{work_id}/characters/{id} # 人物档案
GET /api/works/{work_id}/era            # 时代分析
GET /api/works/{work_id}/author         # 作者分析
GET /api/compare?ids=hamlet,raskolnikov # 人物对比（返回定量数据）
```

API 返回完整数据（不做剧透过滤）。剧透过滤逻辑在前端实现——外部调用方如果要做自己的过滤，可以根据 `scene_annotations[].chapter` 和 `spoiler_level` 字段自行处理。

---

## 七、分阶段路线图

### Phase 0：原型验证（2–3 周）

**目标：** 用 2 本书验证三层分析框架的可行性。

- 第一本：**《红楼梦》**——完整体验中文经典的三层分析。人物众多、心理层次丰富、清代社会语境充足、曹雪芹个人经历与作品的映射被红学充分讨论。可以做贾宝玉、林黛玉、薛宝钗、王熙凤、贾母、晴雯六个人物。
- 第二本：**《罪与罚》**——验证跨文化分析能力。陀思妥耶夫斯基的心理描写本身就具有高度心理学价值；沙俄时代的司法和社会结构提供了丰富的 L2 素材；陀氏的西伯利亚流放经历和个人信仰挣扎是 L3 的上佳素材。可以做拉斯柯尔尼科夫、索尼娅、波尔菲里、斯维德里盖洛夫等人物。
- 手工 + AI 辅助生成 3–5 个人物档案、1 份时代分析、1 份作者分析（每本书）
- 不建网站——先用 JSON + Markdown 文件输出，用简单 HTML 预览阅读体验
- 找 5–10 个读者试用，收集反馈："这个分析帮助你理解人物了吗？""剧透处理合理吗？""哪里让你觉得'过度解读'了？""你最想分享给朋友的是哪个部分？"
- **产出：** 经过真实读者验证的 schema v1.0、prompt 模板（中英双语）、质量检查清单

### Phase 1：MVP 网站（4–6 周）

**目标：** 一个可以公开访问的双语网站，包含 2 本书的完整三层分析和核心交互。

- Next.js 项目搭建，Tailwind 配置，基础组件库
- 中英双语路由（`/zh/work/...` 和 `/en/work/...`）
- 人物档案页（含进度门禁、雷达图、关系图谱、行为注解、剧透折叠）
- 时代分析页
- 作者表达页
- 三层之间的导航链接
- 首页（作品列表 + 项目介绍 + "开始探索"入口）
- Vercel 部署
- **产出：** 上线可用的网站，包含 2 本书 × 3 层分析 × 2 种语言

### Phase 2：对比与传播（4–6 周）

**目标：** 支持跨作品对比和社交传播。

- 人物对比页（雷达图叠加、大五维度排名）——核心增长引擎
- 排行榜/探索页（"文学中最神经质的十个主角""防御机制使用排行"等）——搜索流量入口
- 分享卡片（Open Graph 图片自动生成——雷达图 + 人物名 + 一句话总结）
- 响应式优化（移动端体验——大多数读者从手机访问）
- **产出：** 可以病毒传播的网站

### Phase 3：开放贡献（4–6 周）

**目标：** 建立贡献者社区和自动化审核管线。

- 贡献指南和模板完善（双语）
- JSON schema 自动校验 CI
- 贡献者排行榜/致谢页
- 外部 API 正式发布
- 贡献者文档（如何写一份好的人物档案）
- 目标：5+ 本书的内容
- **产出：** 可持续运作的开放内容项目

---

## 八、版权边界

### 8.1 作品选择

- **优先公版书。** 在中国，公版书的定义是作者去世超过 50 年（著作权法第 23 条）。1928 年之前出版的外国作品在美国也已进入公有领域。
- **版权期内作品。** 可以分析，但网页不展示原文引用全文——只展示章节号索引 + 短引用（合理使用）。这限制了 L1 的 `citations` 字段，但不影响分析本身。也限制源材料的存储——不能托管完整的版权期文本。

### 8.2 分析文本

人物心理分析、时代语境分析和作者表达分析都是**原创内容**，不属于翻译或改编。按 CC BY-NC-SA 4.0 发布，与 LifeBook 书坊的内容授权保持一致。

### 8.3 AI 生成的内容

AI 生成的分析初稿需要人工审校后才能发布。发布版本标注生成者（"AI 初稿 + 张三审校"），不将 AI 输出直接作为最终发布版。

---

## 九、最终决策

1. **项目名称：** Life in Book。
2. **试点书：** 《红楼梦》和《罪与罚》——一中一西，一诗性一心理，覆盖两种核心分析风格。
3. **传播策略：** 学术为底，通俗为面。心理学框架不删，但表达用故事化叙事。免责声明放在页面底部（诚实但不扫兴）。定量数据（雷达图、排行榜）作为传播抓手。
4. **语言：** 中英双语，独立撰写两套档案（不是翻译）。结构化字段（key）用英文，内容字段（value）有 zh-CN 和 en 两个版本，存储为独立文件。
5. **人格维度：** 保留大五人格 + 黑暗三人格。页面底部标注"以上分析基于心理学框架对虚构人物的解读，仅供阅读辅助，不构成临床诊断"。这个声明不前置——读者读到一半的流畅体验比合规焦虑更重要。

### 6. 内容存储格式

**决定：Markdown + YAML frontmatter。**

定性分析是长篇叙事，Markdown 比 JSON 更适合撰写、浏览和 Git diff。定量数据和结构化元信息放在 YAML frontmatter 中。一份档案文件的结构：

```markdown
---
character_id: lin-daiyu
character_name: 林黛玉
character_name_en: Lin Daiyu
work_id: hongloumeng
work_title: 红楼梦
work_title_en: Dream of the Red Chamber
profile_version: 1.0.0
last_updated: 2026-07-06
big_five:
  openness: 9.0
  conscientiousness: 4.0
  extraversion: 2.5
  agreeableness: 3.5
  neuroticism: 9.5
percentiles:
  neuroticism_percentile: 98
  openness_percentile: 95
---

# 林黛玉 · 人物心理档案

## 心理画像

林黛玉是一个高度敏感的灵魂被置于一个注定衰落的贵族家庭中……
```

构建时，Next.js 使用 `gray-matter` 解析 frontmatter 获取定量数据，用 `marked` 或 `remark` 将正文转为 HTML。

### 7. 译本与引用策略

**中文档案引用中文权威译本，英文档案引用英文权威译本。每份档案在 frontmatter 中声明所引用的版本。**

| 作品 | 中文引用版本 | 英文引用版本 |
|------|------------|------------|
| 红楼梦 | 人民文学出版社 1982 年版（以庚辰本为底本） | David Hawkes, *The Story of the Stone* (Penguin, 1973–1986) |
| 罪与罚 | 上海译文出版社 朱海观/王汶 译 | Richard Pevear & Larissa Volokhonsky (Vintage, 1993) |
| 后续中国古典作品 | 以权威整理本为准 | 以学界公认最佳英译本为准 |
| 后续外国作品 | 以学界公认最佳中译本为准 | 以权威英译本/原文为准 |

对于中文古典（如《红楼梦》），引用时标注回数（如"第三回""第二十七回"），不标注页码——因为不同版本的分页不同，但回目是稳定的。对于外国小说，标注章节号。

### 8. 剧透层级

**决定：四级制 + 文化共识标记。**

| 级别 | 含义 | 前端表现 |
|------|------|---------|
| `none` | 不涉及剧情信息，仅涉及人物一般特征（如"敏感、多愁善感"） | 始终可见 |
| `context` | 涉及场景氛围和人物状态，但不泄露具体事件结果 | 对未设置阅读进度的用户折叠；设置了进度的用户，进度到达前折叠 |
| `plot` | 涉及具体情节事件，但不涉及结局或重大转折 | 严格按章节进度折叠 |
| `climax` | 涉及重大转折、死亡、结局 | 双重保护：按章节进度折叠 + 额外点击确认提示"以下内容涉及全书最关键的剧情转折，确定查看？" |

`context` 级别的引入解决了《红楼梦》这种经典作品的困境："黛玉忧郁敏感"不算剧透，"第 27 回葬花并作葬花吟"属于 `context`——透露了场景但几乎所有中文读者都听说过葬花——但前端仍然折叠，只是折叠提示语用较温和的语气："以下内容涉及本书后续章节的场景描写"而非"⚠️ 以下内容包含剧透"。

每个档案条目额外附加一个布尔字段 `cultural_common_knowledge`。为 `true` 时，前端仍然遵循剧透折叠逻辑，但提示文字从"⚠️ 以下内容包含剧透，将揭示后续剧情发展"降级为"以下内容涉及经典场景，如果你希望保持完全未知的阅读体验，可以跳过"。

---

## 十、定稿说明

本文档为 Life in Book 项目的设计定稿（v1.0.0）。Phase 0 原型验证阶段的目标不变：用《红楼梦》和《罪与罚》的实际档案写作来验证三层分析框架、存储格式和贡献流程的可行性。期间 schema 的细节（如 field name、定量维度数量、引用格式）可以根据实际写作体验微调，但核心架构——三层分析、渐进式披露、中英双语独立档案、Markdown+YAML 存储——不再变动。
