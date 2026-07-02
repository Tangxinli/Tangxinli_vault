---
name: ljg-people
description: >-
  CEO办公室人事决策分析。帮助CEO办公室负责人对关键人事决策（调整、转岗、任用、晋升）进行结构化分析，
  生成包含CEO视角和当事人心理的八步判断简报，供内部决策参考。
  Use when user says '人事决策', '人的决策', '帮我分析这个人', '怎么调整', '怎么用', '用谁', 
  '任用分析', '这个人该怎么处理', or provides documents/transcripts about a personnel decision 
  they need to advise the CEO on.
---

# 人事决策分析

为 CEO 办公室负责人生成关键人事决策的八步判断简报。

## 核心理念

人的决策不只是能力判断——是在特定的政治结构和信任关系里，找到对所有关键方代价最小、
实现可能最大的路径。

好的分析不是"这个人好不好"，而是三个问题：
- CEO 真正在意什么（不是他说他在意什么）
- 当事人会怎么反应（不是他该怎么反应）
- 什么路径在这个组织里走得通

## 输入格式支持

接受以下任意格式，可混合提供：

- **口头描述**：自然语言讲述情况
- **结构化字段**：人物 / 决策类型 / 背景 / 关系 / 约束条件
- **文件材料**：会议纪要、沟通记录、内部公告、绩效文档、对话录音文字稿

### PDF 文件处理

```python
import pdfplumber
with pdfplumber.open("path") as pdf:
    text = "\n".join(page.extract_text() or "" for page in pdf.pages)
```

### Word 文件处理

```python
from docx import Document
doc = Document("path")
text = "\n".join(p.text for p in doc.paragraphs if p.text.strip())
```

## 决策类型识别

从输入中识别并标注以下类型，分析时相应调整 ⑤ 当事人心理 的侧重：

| 类型 | 说明 |
|------|------|
| 调整/转岗 | 原岗不适任，需平移或降维 |
| 任用 | 为关键岗位选人 |
| 晋升 | 现有人才的级别跃升 |
| 离场管理 | 高层退出或离职的处理方式 |

---

## 分析框架：八步结构

每步都要基于输入信息实质作答。信息不足处直接标注，不硬撑。

### ① 处境全景

从这个人的角度看清楚他现在在哪里：

- **基本信息**：角色、年限、在公司的标签与定位
- **历史贡献**：他真正做出了什么，组织当时为什么需要他
- **当前状态**：现在为什么成为问题，或为什么需要变化
- **关系结构**：与 CEO、创始人、关键同僚的信任位置与政治站位

### ② CEO 视角

CEO 作为决策者，有其特定处境和天然的思维滤镜。这一节帮你想清楚 CEO 会怎么看这件事。

**CEO 一定会考虑的：**
- 这件事对其他高管的信号意义（"CEO 是这样处理这类人的"）
- 对创始人、董事会或上级的交代逻辑
- 业务连续性风险（岗位空窗期如何处理）
- 这个决定对自己管理信誉和一致性的影响
- 5 年后回头看，这是不是他愿意承认的决定

**CEO 不太会主动想到的（你需要帮他想的）：**
- 当事人的实际感受和面子需求
- 执行时机和沟通的具体措辞细节
- 当事人在组织内的情感网络（他的人会怎么反应）
- 短期阵痛的实际承受度

### ③ 决策难点

直接说出这个决策的核心张力——不是罗列困难，是找到那个真正让决策复杂的东西：

- 是能力问题（但情感账很厚）？
- 是情感问题（但业务上还有价值）？
- 是政治问题（但没有公开说得过去的理由）？
- 是时机问题（现在动还是等一等）？

### ④ 选项与代价

列出真实的选项，包括"不动"这个选项：

| 选项 | 主要代价 | 谁受影响最大 | 可行性 |
|------|---------|------------|-------|
| 选项A | ... | ... | 高/中/低 |
| 选项B | ... | ... | 高/中/低 |
| 不做任何动作 | ... | ... | — |

### ⑤ 当事人心理

这个人遇到这件事，他天然会怎么想——不是他该怎么想。

**调整 / 转岗 / 离场场景：**
- **尊严与面子**：外部如何解释这件事？在他人眼中是"被抛弃"还是"功成身退"？
- **实际利益**：级别、收入、头衔、退出条件——他的底线在哪里？
- **最深的担忧**：彻底被边缘化？还是过去的贡献不被承认？
- **未说出口的需求**：被郑重道谢、被公开认可、被有尊严地对待

**任用 / 晋升场景：**
- **兴奋背后的焦虑**：我为什么被选中？对我的期望是什么？
- **最担心的事**：资源是否配套？授权是否真实？有没有人托底？
- **驱动力来源**：是外部压力驱动还是内在想做这件事？
- **需要但不会说的**：CEO 真的相信我，还是我只是个备选？

### ⑥ 建议路径

给出一个明确的推荐，不骑墙：

- **推荐什么**：具体方案（不是"可以考虑"）
- **核心理由**：用前面的分析支撑，不重新编理由
- **成立的前提条件**：这个方案在什么前提下才走得通
- **最大风险点**：这个推荐最可能在哪里出问题

### ⑦ 关键对话

哪几次谈话将决定这件事能不能走通：

每次对话说明：
- **谈话目标**：不是"让他接受"，是具体要确认或传达什么
- **绝对不能说的话**：及原因
- **最可能出现的对抗点**：以及如何应对

### ⑧ 预案

最可能出错的 1-2 个场景：

- 当事人的反应超出预期，会是什么样？
- 组织内的反应超出预期，会是什么样？
- 每种情况下，提前准备什么？

### ⑨ 向CEO汇报的沟通稿

基于前八步分析，生成一份可以直接使用的沟通准备稿。

**结构说明**：CEO 已经在思考这件事，不需要你帮他回顾背景。
最有效的结构是"结论→支撑→难点→请求"——在3分钟内给他足够的信息做判断，
多余的部分等他问。

---

**第一步：结论（10秒）**

直接说你的建议，第一句话就是结论。

模板：「关于[人名]，我的建议是[具体行动]。」

禁止开头出现：「这个情况比较复杂」「我觉得需要好好研究」「有几个方向可以考虑」

---

**第二步：两个关键支撑（60-90秒）**

从八步分析中，挑出CEO最会在意的那两个理由。
不是你觉得分析最精彩的两个——是他的视角里最有分量的两个。
参考 ② CEO视角 和 ③ 决策难点 来选。

格式：「有两个核心原因——第一，[支撑A]；第二，[支撑B]。」

---

**第三步：一个核心难点（30秒）**

主动说出这件事最难处理的地方。这不是在动摇你的建议，
而是让CEO信任你想得全面，他不会被没说的东西吓到。

模板：「这件事最复杂的地方是[X]，因为[Y]。」

参考 ③ 决策难点 和 ⑤ 当事人心理 来选。

---

**第四步：一件事需要你（15秒）**

结尾必须有一个明确的请求或确认，且只有一件事。
必须包含「这样我就可以推进[具体下一步]」——让CEO知道他的决定会推动什么。

模板：「我需要你告诉我/确认[X]，这样我就可以[Y]。」

---

**本次对话不要说的话（从 ⑦ 关键对话 中提取 2-3 条）**

列出具体的话或表达方式，以及不能说的原因。

---

## 输出

生成两个文件（先 HTML，再 org）：

### HTML 文件

- **路径**：`output/relationship/`（若不在项目环境则使用 `~/Desktop/`）
- **命名**：`YYYYMMDDTHHMMSS--人事决策-人名或关键词.html`
- **风格**：Notion 风格，`background: #f7f6f3`，`color: #37352f`，最大宽度 720px，居中
- **顶部工具栏**：固定，高度 52px，右侧两个按钮：
  - 「保存长图」（白色描边按钮）
  - 「复制图片·粘贴到微信」（绿色 `#07c160` 主按钮）
- **html2canvas CDN**：`https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js`

**HTML 内容顺序**：

1. 标题 + 元信息（人名、决策类型、日期）
2. **⑨ 向CEO汇报的沟通稿**（用 `.brief-block` 样式，放在最顶部，打开文件第一眼看到）
3. 分隔线
4. ①—⑧ 八步分析（依次展开，作为沟通稿的支撑材料）

**按钮逻辑（标准模板）：**

```javascript
function showToast(msg, duration = 2800) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), duration);
}

async function renderCanvas() {
  const el = document.getElementById('main-content');
  return html2canvas(el, {
    scale: 2, useCORS: true,
    backgroundColor: '#f7f6f3',
    logging: false, windowWidth: 800
  });
}

async function saveImage() {
  showToast('正在生成长图，请稍候…', 8000);
  try {
    const canvas = await renderCanvas();
    const link = document.createElement('a');
    link.download = 'FILENAME.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
    showToast('图片已保存，可拖入微信发送 ✓');
  } catch (e) { showToast('生成失败，请重试'); console.error(e); }
}

async function copyImage() {
  showToast('正在生成图片，请稍候…', 8000);
  try {
    const canvas = await renderCanvas();
    canvas.toBlob(async (blob) => {
      try {
        await navigator.clipboard.write([new ClipboardItem({ 'image/png': blob })]);
        showToast('图片已复制 ✓  在微信聊天框 Cmd+V 粘贴即可');
      } catch (err) {
        showToast('剪贴板权限不足，已自动改为下载长图');
        const link = document.createElement('a');
        link.download = 'FILENAME.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
      }
    }, 'image/png');
  } catch (e) { showToast('生成失败，请重试'); console.error(e); }
}
```

**CSS 块样式**（每节对应色彩）：

```css
/* 沟通稿 — 深色底，置顶视觉锚 */
.brief-block {
  background: #1e1e1e;
  color: #f0efe9;
  padding: 28px 32px;
  border-radius: 12px;
  margin: 0 0 40px 0;
}
.brief-block h3 {
  color: #fff;
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-bottom: 20px;
  opacity: 0.5;
}
.brief-block .brief-step {
  margin-bottom: 20px;
}
.brief-block .brief-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #9b9690;
  margin-bottom: 6px;
}
.brief-block .brief-content {
  font-size: 15px;
  line-height: 1.7;
  color: #f0efe9;
}
.brief-block .brief-avoid {
  margin-top: 20px;
  padding-top: 16px;
  border-top: 1px solid rgba(255,255,255,0.1);
  font-size: 13px;
  color: #9b9690;
}

/* CEO视角 — 蓝色 */
.ceo-block {
  background: #f0f7ff;
  border-left: 4px solid #4a9eff;
  padding: 20px 24px;
  border-radius: 0 8px 8px 0;
  margin: 24px 0;
}

/* 当事人心理 — 紫色 */
.person-block {
  background: #f8f4ff;
  border-left: 4px solid #9b6fff;
  padding: 20px 24px;
  border-radius: 0 8px 8px 0;
  margin: 24px 0;
}

/* 建议路径 — 绿色 */
.action-block {
  background: #f0faf4;
  border-left: 4px solid #34b87a;
  padding: 20px 24px;
  border-radius: 0 8px 8px 0;
  margin: 24px 0;
}

/* 决策难点 / 核心判断 — 橙色 */
.insight-block {
  background: #fffbf0;
  border-left: 4px solid #f5a623;
  padding: 20px 24px;
  border-radius: 0 8px 8px 0;
  margin: 24px 0;
}

/* 引用原话 */
.quote-block {
  background: #f9f8f6;
  border-left: 3px solid #b8b3ab;
  padding: 16px 20px;
  border-radius: 0 6px 6px 0;
  margin: 20px 0;
  font-style: italic;
  color: #5a5650;
}
```

### Markdown 文件

- **路径**：`~/Documents/Obsidian Vault/3-Output/`
- **命名**：`YYYYMMDDTHHMMSS--人事决策-人名或关键词__people.md`
- **格式**：Markdown

```markdown
---
title: "人事决策：{描述}"
date: "{日期}"
tags: [人事决策]
identifier: "{timestamp}"
---

# 零、向CEO汇报的沟通稿
## 结论（第一句话）
## 两个关键支撑
## 一个核心难点
## 一件事需要你
## 本次对话不要说的话
# 一、处境全景
# 二、CEO 视角
## CEO 一定会考虑的
## CEO 不太会主动想到的
# 三、决策难点
# 四、选项与代价
# 五、当事人心理
# 六、建议路径
# 七、关键对话
# 八、预案
```

两个文件写完后，向用户报告完整路径。

---

## 生成规则

1. 基于提供的信息分析，不编造；信息不足处直接标注，不硬撑
2. **敢判断**——建议路径必须给出明确推荐，禁止出现"视情况而定"、"建议充分沟通"
3. CEO 视角和当事人心理两节必须结合具体情境写，不能写成通用框架的复述
4. 选项与代价里，"不动"这个选项必须写
5. 关键对话里，"不能说的话"必须具体——不是"不要激化矛盾"，是具体的话和原因
6. 中文撰写，以说透为准，不计字数
