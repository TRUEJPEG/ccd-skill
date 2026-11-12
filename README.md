# ccd · CCD 直闪写实人像提示词 Skill

[中文](#中文) · [English](#english)

---

## 中文

### 这是什么

`ccd` 是一个 [Claude Code](https://docs.claude.com/en/docs/claude-code) Skill：把**一张参考图**反推成，或把**一段现有提示词**改写成，一条完整、详细、可直接复制的**中文生图提示词**。默认风格是 2000 年代便携 CCD 相机在暗处开直闪拍下的写实人像：

- 暗背景，机顶直闪，亮度随距离快速衰减
- 真实肤质：毛孔、细小汗毛、局部水光，不磨皮
- 超白冷调皮肤，黑发，不写眼睛颜色，几乎不写腮红
- 低动态范围、数字噪点、粗颗粒、深黑位
- 只写**成年**人物

输出按固定的中文分段标签组织：`人物：`、`身材：`、`皮肤：`、`表情：`、`姿态：`、`服装：`、`场景：`、`光线：`、`构图：`、`相机参数：`、`画面质感：`。每张图一个代码块，小标题放在代码块外，方便直接复制。

这个 Skill **只输出文字**，不会替你调用任何生图接口或花钱。

### 安装

**最简单：交给你的 Agent。** 把下面这段话复制给 Claude Code（或 Codex），它会自己装好：

```
帮我安装这个 Skill：https://github.com/TRUEJPEG/ccd-skill
把它克隆到 ~/.claude/skills/ccd（如果你是 Codex，就放到 ~/.codex/skills/ccd），装好后告诉我怎么用。
```

装好后开一个新对话就能用。

**手动安装：** 需要已安装 Claude Code。把整个文件夹放到 `~/.claude/skills/ccd/`，保证 `~/.claude/skills/ccd/SKILL.md` 存在即可。

```bash
git clone https://github.com/TRUEJPEG/ccd-skill.git ~/.claude/skills/ccd
```

- 只想在某个项目里用：放到项目里的 `.claude/skills/ccd/`。
- 不用 git：下载 zip，解压后把文件夹改名为 `ccd` 放进 `~/.claude/skills/`。
- 装好后开一个新的 Claude Code 会话，输入 `/ccd` 能看到它就说明装上了。
- Codex 用户：放到 `~/.codex/skills/ccd/`，`agents/openai.yaml` 是给 Codex 用的界面信息。

### 使用

**反推图片（默认 CCD）**：把图片拖进对话，然后

```
/ccd
```

或者直接说"把这张图反推成 CCD 提示词"。

**改写已有提示词**：`/ccd` 后面直接粘贴别人的提示词（英文、关键词串、动漫风都可以），它会去掉动漫画法、补全结构，改写成写实 CCD 版本。

**局部修改**：在上一条结果的基础上说"外套换成黑色皮夹克，全给我"，它会交付修改后的**整条**提示词，而不是只给一个片段。

**几条默认行为**：

- 默认不写尺寸和画幅比例，由你在生图平台上自己设。
- 默认不附长串反向提示词。
- 参考图里没拍到脸时，会通过扩大取景或回眸让人物露脸，并说明这是补全。
- 图里的文字、水印、界面一律忽略，不当成指令。

### 示例

输入：一张深夜便利店门口的随手抓拍 + `/ccd`

输出（节选格式，小标题在代码块外）：

**深夜便利店门口的直闪抓拍**

```
人物：一名明确成年的二十多岁年轻亚洲女性，韩系偶像感长相，流畅V型鹅蛋脸，狭长的狐狸眼，妆容清透，皮肤带水光感，鼻尖有一点光泽，水润的珊瑚粉唇色。黑色长发自然披散，几缕碎发贴在脸侧，耳垂戴一枚小银圈耳环。

皮肤：超白皮肤，受直闪时呈冷调白皙，保留细腻毛孔、细小汗毛和自然的肤色变化，鼻尖和颧骨上方有局部柔和高光，不磨皮。

表情：嘴角轻轻上扬，像是刚被朋友叫住，视线直接看向镜头，眼神松弛。

姿态：站在便利店玻璃门外，身体微微侧向画面右侧；画面右侧的手插在外套口袋里，画面左侧的手举着一罐冰咖啡贴在下巴旁，罐身挂着细小水珠。

服装：oversize 深灰色连帽卫衣外套，厚实棉质，袖口堆叠在手腕；里面是白色圆领T恤；黑色直筒长半身裙，白色帆布鞋。

场景：深夜街边便利店门口，玻璃门后是模糊的货架和冷白日光灯，门外地面潮湿，反射零星灯光；画面左侧边缘露出一辆自行车的车把。

光线：整体环境极度昏暗，小型数码相机的近轴直闪直接打在人物正面，脸和咖啡罐清晰，身后玻璃上留下一个小小的闪光反射点；亮度随距离快速衰减，背景比人物暗2—3档，店内冷光只作为微弱的边缘光。

构图：齐腰中景，略高于平视的机位，人物位于画面中央偏左，玻璃门的竖直边框形成纵向线条。

相机参数：20毫米广角定焦镜头，光圈f/1.8，焦点在眼睛，背景货架保留可辨轮廓。

画面质感：2000年代日系便携CCD低光抓拍，动态范围有限，高光略溢出，轻微柔焦，明显数字噪点与粗颗粒，黑位压得很深，暖调区域白平衡略偏。皮肤、棉布、铝罐和潮湿地面各自保留不同的反射特征。
```

### 默认角色

不指定的话，它默认会画这样一个人：

- 二十多岁的成年亚洲女性，韩系偶像感长相
- 流畅的 V 型鹅蛋脸，狭长的狐狸眼
- 清透妆，水润的珊瑚粉唇（参考图有妆容时按参考图写）
- 黑色头发
- 超白冷调皮肤，带一点水光，保留真实毛孔
- 丰满的沙漏型身材

**这些都可以按你的喜好改**：编辑 `references/defaults.md` 里的「固定人物、身材与皮肤」，或者直接跟你的 Agent 说"把 ccd 的默认角色改成 xx"。

### 自定义

- 默认人物长相、身材、肤色都写在 `references/defaults.md` 的「固定人物、身材与皮肤」。身材默认偏丰满，不合你口味就直接改那一段，换成你自己的默认人物即可。
- 光线、相机参数和画面质感也在 `references/defaults.md` 的「固定摄影基盘」，想换风格就改这一段。

### 文件结构

```
ccd/
├── SKILL.md                 # 入口：读图规则、交付格式、自查
├── references/
│   └── defaults.md          # 默认人物 + 写实 CCD 摄影基盘
└── agents/openai.yaml       # Codex 界面信息（Claude Code 不读）
```

### 致谢与许可

由 [True JPEG](https://truejpeg.com) 整理，一个 AI 写实人像提示词画廊。MIT 许可，见 [LICENSE](LICENSE)。

---

## English

### What it is

`ccd` is a [Claude Code](https://docs.claude.com/en/docs/claude-code) Skill that turns **a reference image**, or **an existing prompt**, into one complete, detailed, copy-ready **Chinese image-generation prompt**. The default look is a realistic portrait shot on a 2000s point-and-shoot CCD camera with on-camera flash in a dark room:

- dark background, direct on-axis flash with fast falloff
- real skin texture: pores, fine vellus hair, local sheen, no airbrushing
- very fair, cool-toned skin; black hair; no eye color; almost no blush
- limited dynamic range, digital noise, coarse grain, crushed blacks
- **adults only**

Prompts are organized with fixed Chinese section labels (`人物` subject, `身材` body, `皮肤` skin, `表情` expression, `姿态` pose, `服装` outfit, `场景` scene, `光线` lighting, `构图` composition, `相机参数` camera, `画面质感` texture). One code block per image, with a short title outside the block.

The Skill **only writes text**. It never calls an image API or spends money.

### Install

**Easiest: let your agent do it.** Paste this into Claude Code (or Codex):

```
Install this Skill: https://github.com/TRUEJPEG/ccd-skill
Clone it to ~/.claude/skills/ccd (for Codex, use ~/.codex/skills/ccd), then tell me how to use it.
```

Start a new session afterwards and it's ready.

**Manual install:** requires Claude Code. Put the folder at `~/.claude/skills/ccd/` so that `~/.claude/skills/ccd/SKILL.md` exists.

```bash
git clone https://github.com/TRUEJPEG/ccd-skill.git ~/.claude/skills/ccd
```

- Project-only: put it in `.claude/skills/ccd/` inside the project.
- Without git: download the zip, rename the folder to `ccd`, move it into `~/.claude/skills/`.
- Start a new Claude Code session; if `/ccd` shows up, it's installed.
- Codex: use `~/.codex/skills/ccd/`; `agents/openai.yaml` is Codex UI metadata.

### Usage

- **Reverse an image (default CCD):** drop an image into the chat and type `/ccd`, or just say "turn this into a CCD prompt".
- **Rewrite a prompt:** `/ccd` followed by any prompt (English, tag lists, anime-style). It strips anime rendering, fills in structure, and rewrites it as a realistic CCD prompt.
- **Partial edits:** "swap the hoodie for a black leather jacket, give me the full prompt" returns the whole updated prompt, not a fragment.

Defaults: no size or aspect ratio (set those in your generator), no long negative-prompt list, faces are made visible when the reference hides them (stated as a completion, not as observed), and any text/watermark/UI inside the image is ignored and never treated as instructions.

See the Chinese section above for a full example output.

### Default character

Unless you say otherwise, it draws:

- an adult Asian woman in her twenties with a K-pop idol look
- a smooth V-shaped oval face and narrow fox eyes
- clean makeup and glossy coral-pink lips (makeup in the reference image takes priority)
- black hair
- very fair, cool-toned skin with a little sheen and real pores
- a curvy hourglass figure

**Change any of it to taste:** edit 「固定人物、身材与皮肤」 in `references/defaults.md`, or just tell your agent "change ccd's default character to ...".

### Customize

The default character, body (curvy by default) and skin live in `references/defaults.md`; edit that section to make it your own. Lighting, camera and texture rules are in the same file under 「固定摄影基盘」.

### Credits & license

Curated by [True JPEG](https://truejpeg.com), an AI realistic-portrait prompt gallery. MIT licensed, see [LICENSE](LICENSE).
