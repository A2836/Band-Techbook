# 校园乐队舞台技术手册

**TRYBAND · Campus Band Tech Handbook · 2026**

> 线上阅读：<https://a2836.github.io/Band-Techbook/>

写给刚加入社团、准备第一次上台的校园乐队成员。它不要求你先懂调音台，而是从「你要做什么、和谁沟通、怎么检查」开始，
把一场演出拆成可以准备的动作：谁负责什么、歌怎么统一版本、PGM 怎么导出、返听要什么、走台按什么顺序、出问题先查哪一段。
14 章、117 小节，约 3.6 万字，通读约 90 分钟——更常见的用法是演出前翻到对应那一章。

---

## 目录

| 章 | 标题 | 内容 |
| --- | --- | --- |
| 01 | [成团：先把"谁会做什么"说清楚](https://a2836.github.io/Band-Techbook/#/ch/01) | 编制、角色与最小可行配置，第一次成团会议要定下的事 |
| 02 | [选曲与排练准备](https://a2836.github.io/Band-Techbook/#/ch/02) | 怎么选歌、定调、统一参考录音 |
| 03 | [排练：个人先练熟，合排再磨配合](https://a2836.github.io/Band-Techbook/#/ch/03) | 排练节奏、反馈方式、录像与多轨录音 |
| 04 | [声音信号链：从乐器到观众耳朵](https://a2836.github.io/Band-Techbook/#/ch/04) | 拾音、DI、接口箱、调音台与主扩 |
| 05 | [技术文档](https://a2836.github.io/Band-Techbook/#/ch/05) | Stage Plot、Input List、Tech Rider、Monitor List |
| 06 | [PGM：把伴奏做成可靠的现场资产](https://a2836.github.io/Band-Techbook/#/ch/06) | 导出、命名、播放、备份、click 与语音 cue |
| 07 | [返听：让每个人听见自己需要的声音](https://a2836.github.io/Band-Techbook/#/ch/07) | 监听分配、IEM、音量与听力保护 |
| 08 | [演出资源：校园、校外与线上渠道](https://a2836.github.io/Band-Techbook/#/ch/08) | 机会从哪来，怎么判断值不值得接 |
| 09 | [主办方对接](https://a2836.github.io/Band-Techbook/#/ch/09) | 询价、advance、变更记录 |
| 10 | [走台与 Soundcheck](https://a2836.github.io/Band-Techbook/#/ch/10) | 到场、line check、口令，时间不够时先保什么 |
| 11 | [演出当天](https://a2836.github.io/Band-Techbook/#/ch/11) | 时间表、台上沟通、换场与收尾 |
| 12 | [现场故障排查](https://a2836.github.io/Band-Techbook/#/ch/12) | 从"没声音"到"PGM 不响"，按信号链定位 |
| 13 | [安全、听力与团队协作](https://a2836.github.io/Band-Techbook/#/ch/13) | 电气与人身安全、听力保护、说清问题 |
| 14 | [模板、清单与术语速查](https://a2836.github.io/Band-Techbook/#/ch/14) | 可直接抄走的模板、检查表与中英术语对照 |

---

## 怎么用这个站

- **首页**是章节索引，点任意卡片进入；右上角「目录」（快捷键 <kbd>K</kbd> 或 <kbd>/</kbd>）随时唤出全部章节。
- **一章一页**：桌面左侧是本章节小节目录，跟随滚动高亮；章末有上一章 / 下一章。
- **键盘**：<kbd>K</kbd> 开合目录，<kbd>←</kbd> <kbd>→</kbd> 翻章，<kbd>Esc</kbd> 关闭。
- **手机**：底部固定「上一章 / 目录 4/14 / 下一章」，长文里也能随时跳走。
- **深链**：每章有独立地址，可以直接发给别人，例如
  [`#/ch/12`](https://a2836.github.io/Band-Techbook/#/ch/12)；章内小节锚点形如 `#sub-4-3`。
- 顶部细红线是阅读进度。
- 站内不提供打印入口（按需求移除）；原始 PDF / Word 版本由维护者本地留存。

## 技术实现

整站是**一个自包含的 HTML 文件**：CSS、JS、SVG 全部内联，没有任何外部请求，断网也能打开，
拷到 U 盘或邮件附件里同样可用。

- **组件**：[React 18](https://react.dev/) + [reacticle](https://github.com/ConardLi/garden-skills) 组件协议（`Article` / `Section` / `Table` / `Aside` 等），主题为 `vignelli`。
- **内容**：14 个章节组件，图表是手写 SVG 与 CSS 网格，不依赖图片资源。
- **路由**：hash 路由（`#/ch/04`），纯前端，GitHub Pages 不需要 404 兜底。
- **构建**：esbuild 打包后把 JS/CSS 内联进 `index.html`（`scripts/build.mjs`），产物 756 KB、gzip 约 214 KB。
  构建时剔除 reacticle 自带的 KaTeX 数学字体（约 1.4 MB，本站没有公式）。
- **适配**：320–1440 px 全区间无横向溢出；支持 `prefers-reduced-motion`；跳转链接、焦点管理、`aria-live` 章节播报。

## 维护与发布

内容源文件保存在维护者的本地项目里（`article/sections/*.tsx`、`article/site/*`），本仓库只存放构建产物。

```bash
# 构建（在本地项目目录）
node scripts/build.mjs     # 或 npm run build
npm run typecheck          # TypeScript 检查

# 发布：把 dist/index.html 覆盖到本仓库根目录的 index.html
# 提交到 main 后，GitHub Pages 会自动发布，约 30–60 秒生效
```

改动内容时注意：

1. 每章的 `Section index/title` 与 `article/site/chapters.tsx` 里的章节元数据（标题、小节数、阅读时长）要保持一致——
   导航、索引卡片、页头信息都读后者。
2. 阅读时长按渲染后正文约 380 字/分钟估算，改完正文记得复核。
3. 新增章节需要在 `article/site/chapters.tsx` 登记，并更新首页的「14 章 · 117 节」计数。

## 贡献

手册会跟着每一届乐队继续更新。发现某章的流程和你们学校的实际情况不符，欢迎直接改那一章——
把「我们学校是怎么做的」写清楚，比追求通用表述更有用。

## 许可与致谢

- 内容 © 2026 TRYBAND，社团内部技术文档；转载或引用请注明来源。
- 页面框架基于 [reacticle](https://github.com/ConardLi/garden-skills) 的 `vignelli` 主题，
  取自 beautiful-article 组件协议。
- 所有示意图（信号链、使用路径、舞台布局）为本项目自制。

## 更新记录

- **2026-10-22** 重构为分章网页版：新增首页索引、章节路由、吸顶导航与目录抽屉、手机底部导航、阅读进度；
  移除打印入口，构建体积从 2.1 MB 降到 756 KB。
- **2026-10** 初版上线（单页长文）。
