# 290354

一边改 KataGo 的 C++ 搜索层，一边跑一条科普动画流水线：选题侦察 → 三轴打分 → 技术路线选型 → 逐帧渲染 → 音画对齐 → 踩坑留档。

不堆实拍、不套模板，每个镜头、每个乘子都是一行一行写出来的。

---

## 引擎与搜索

| 仓库 | 内容 | 规格 |
|---|---|---|
| [fengminggo](https://github.com/290354/fengminggo) | KataGo v1.16.1 让子（handicap）优化分支。原版搜索与价值标定围绕均势局设计，让子方过于保守；本分支在 PDA 控制器、GTP 层、搜索层三处加自适应，默认开启、可单独关闭，`N<2` 时严格退化为原版。顺手修了原版 `ReportedSearchValues` 默认构造为空导致 `expectedScoreStdev` 读未定义行为的 bug | C++ · 9 子局 severity=0.7075 / 访问量 40→56 · `katago runtests` 全过 |

---

## 科普动画流水线

选题不追热点，追"能解释热点的那把钥匙"。每个仓库都留档：情报样本、三轴打分表、技术路线决策、踩坑记录、已知瑕疵、一键复现命令。

### 正在连载

| 仓库 | 内容 | 规格 |
|---|---|---|
| [science-video-lab](https://github.com/290354/science-video-lab) | 科学爆点视频工坊。首期《一根橡皮筋，凭什么证明钉子不能凭空消失？》讲**同调（Homology）**——为什么选它不选更热的拓扑边缘态：因为它是本季度三条爆点新闻的共同底层语言 | 4′16″ · 1920×1080@60 · Manim CE 0.22 · 全程不用 LaTeX · 原创程序化 BGM |
| [sci-pop-20261101-survivor-planets](https://github.com/290354/sci-pop-20261101-survivor-planets) | 科普爆点动画周刊 **第 1 期**：三颗本不该存在的行星（红巨星幸存悖论，云南大学钱声帮团队）。天文题材走路线 B——HTML+Canvas+Playwright 逐帧渲染，不用 Manim | 5′20″ · 1280×720@30 · 9618 帧 · 音画按 `ts = t × (SCRIPT_T/DUR)` 线性映射，语速变了自动跟 |
| [sci-pop-20261102-mosquito-bite](https://github.com/290354/sci-pop-20261102-mosquito-bite) | 科普爆点动画周刊 **第 2 期**：蚊子的「手术」——为什么你几乎感觉不到它在扎你。口器六根零件、两排错开的齿、唾沫里的三种化学物质 | 4′45″ · 1280×720@30 · 8549 帧 · 6 个场景按语义对齐解说 |
| [sci-pop-20261104-blackhole-sprint](https://github.com/290354/sci-pop-20261104-blackhole-sprint) | 科普爆点动画周刊 **第 3 期**：四十倍——LID-568 的超爱丁顿进食。韦布望远镜看到一个被光撑开的盘，怎么绕过爱丁顿极限 | 5′02″ · 1280×720@30 · 9066 帧 · 含片尾卡 |
| [sci-pop-20261106-glueball](https://github.com/290354/sci-pop-20261106-glueball) | 科普爆点动画周刊 **第 4 期**：零个夸克——BESIII 证实 X(2370) 的主要成分是最轻胶球。从禁闭、胶子吃自己讲到三关证据 | 5′06″ · 1280×720@30 · 9179 帧 · 分镜表由 scenes.json 驱动 |

### 单部成片

| 仓库 | 内容 | 规格 |
|---|---|---|
| [openai-eth-manim](https://github.com/290354/openai-eth-manim) | 3Blue1Brown 风格解读 OpenAI 论文《The Exponential Time Hypothesis is False》——从 3-SAT 到稀疏化、多项式变形、共享测量，把 ETH 被证伪的整条算法链画出来 | 31′47″ · 1920×1080 · 30fps · 14 段 · 无配音 · 底部解说条 · 全片重叠报告为零 |
| [cauchy-functional-equation](https://github.com/290354/cauchy-functional-equation) | 柯西函数方程两版：漫士沉思录风（衬线 / 四色 / 留白 / 逐字浮现）与早期讲课版，含 edge-tts 配音与音画对齐脚本 | 漫士版 9′00″/32 页 · 讲课版 10′50″/35 页 |
| [boids-emergence](https://github.com/290354/boids-emergence) | 鸟群算法与涌现：三条规则如何长出一万只鸟；附《唯一游戏猜想》UGC 场景与浏览器端实时预览 | 8′24″ · 2700 字分镜脚本 |
| [the-day-it-rained](https://github.com/290354/the-day-it-rained) | Three.js + Puppeteer + ffmpeg 程序化短片，全片无实拍，1319 行分镜定义 | 223.4 s · 1920×804 · 24fps |

---

## 工具

| 仓库 | 内容 | 规格 |
|---|---|---|
| [c-drive-cleanup-report](https://github.com/290354/c-drive-cleanup-report) | Windows C 盘空间体检留档：逐层扫描 → 提权清理 → HTML 可视化报告 | PowerShell · HTML |

---

## 做法

- **引擎层**：KataGo C++ 改在 `command/` 与 `search/` 下新增文件，不动既有路径；乘子只放宽不收紧，不写回 `SearchParams`，用户显式参数原样保留。
- **技术路线按题材选**：数学 / 离散几何用 Manim CE 0.22；天文 / 连续量演化用 HTML+Canvas+Playwright 逐帧截图。宁可降配置，不可交半成品。
- **反依赖**：能不用 LaTeX 就不用（公式走 Text+Unicode），BGM 用 numpy/ffmpeg 程序化合成，零第三方音频素材。
- **配音**：edge-tts `zh-CN-YunxiNeural`，语速按片子节奏 ±8%；每部片先做三音色 12 秒试听样本再定档。
- **音画对齐**：剧本时间轴固定，成片时长取解说音频实际总长，线性映射——文案改长改短画面自动跟随，不逐段手调。
- **质量门**：自动扫描全片 Text/Tex 包围盒重叠面积比；拼接前逐段重编码规范化 pts（Manim 非零起点会让 `concat -c copy` 把 256s 记成 567s）。
- **留档**：每个仓库都有"已知问题 / 降级记录"章节——踩过的坑（Manim `-qk` 是 2160p 不是 1080p、Noto Sans CJK 缺 ℤ 字形、wait 写死绝对秒数导致 9:27 超长成片）都写清楚根因和修法。

---

## 正在看 / 正在想

- 围棋引擎：KataGo 搜索在让子 / 非均势局下的退化，PDA、cpuct、FPU、根节点保底访问各自该怎么调。
- 计算复杂性：ETH / SETH / Gap-ETH / NSETH，以及计数算法与多项式方法。
- 拓扑与同调：H₁=Z₁/B₁ 怎么用一根橡皮筋讲明白，以及它怎么当钥匙开其他新闻。
- 涌现与多智能体：Boids、UGC、唯一游戏猜想。
- 科普的"沉思感"怎么做——字体、配色、留白、节奏，和课件感对着干。

---

<sub>本文件位于同名仓库 [`290354/290354`](https://github.com/290354/290354)，会显示在 GitHub 个人主页。</sub>
