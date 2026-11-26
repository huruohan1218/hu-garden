# 小胡的美味页面 T1.2

HU'S LITTLE DIGITAL GARDEN 是基于 Yuragi 第一版迁移的静态个人空间。此目录可独立运行、纳入版本管理和部署。第一版文件保存在上一级目录。

## 本地运行

使用 Node.js 22.12+ 或 24 和 npm。在本目录执行：

```sh
npm ci
npm run dev
```

打开终端显示的本地地址。生产预览用 `npm run build`，然后运行 `npm run preview`。构建输出在 `dist/`。

## 目录与编辑入口

| 路径 | 内容 |
| --- | --- |
| src/pages/ | 首页、相册、手记、作品、关于与日志 |
| src/layouts/Main.astro | 页面骨架、元数据、主题和导航脚本 |
| src/components/ | 页头、页脚、栏目布局、纸条与播放器 |
| src/content/notes/ | Markdown 手记，每个文件生成一个独立网址 |
| src/content.config.ts | 手记字段校验 |
| src/data/ | 公开邮箱、相册、作品、纸条、音乐列表 |
| src/styles/ | 全站色彩、字体、断点、内容与交互样式 |
| public/images/ | 自托管 WebP 插画与相册示意图 |
| public/music/ | 两段本项目合成的 13 秒试听音 |
| .github/workflows/pages.yml | 构建并发布 GitHub Pages |

写手记时可复制现有 Markdown 文件，修改文件名、日期、分类、正文及 `placeholder` 字段。文件名决定网址。首页精选入口位于 `src/pages/index.astro`。相册数据的 id 对应同名 WebP。作品数据的 id 对应详情页。音乐列表每项需要文件名与显示标题，新音频放入 public/music。关于页读取 src/data/site.js 的 email；填写真实、可公开使用的联系邮箱后才会显示邮件按钮。

## 迁移记录

1. 视觉阶段保留旧版昵称、文案与栏目，建立六色主题、本地衬线字体栈、植物图版首页和响应式导航。
2. 内容阶段迁入四个相册主题、三篇示例短文、两个项目条目。真实的本站项目展示实际技术栈；其他示例按占位内容展示。
3. 交互阶段加入可记忆主题、分类与搜索、原生灯箱、阅读进度、音乐播放列表、按访客本地日期选取的纸条与彩蛋。
4. 发布阶段使用静态构建、站点基路径、WebP、延迟加载、分享元数据及部署工作流。

## 素材与隐私

首页图版使用内置 ImageGen 生成：象牙色纸面上的蕨叶、野草与浅色花朵，铜版线描和低饱和水彩。四张相册图来自同一组生成指令：日系胶片风格的花丛、雾山、窗边咖啡与森林湖泊。它们均为示意图。试听音为正弦波和衰减包络合成的原创短句。页面只从本站读取资源；主题偏好写入浏览器 localStorage。若替换为个人素材，先确认授权并清除照片中的 GPS 和其他敏感元数据。

## GitHub Pages

以 **hu-garden 本身**作为仓库根目录。向自己的 GitHub 仓库推送 main 分支。在仓库 Settings → Pages → Build and deployment 选择 GitHub Actions，再在 Actions 中运行 Publish garden。工作流从 Pages 配置读取域名与子目录，执行 npm ci 和静态构建，只上传 dist。部署网址可在工作流的 github-pages 环境中查看。[Astro 的 GitHub Pages 部署说明](https://docs.astro.build/en/guides/deploy/github/)

## Vercel

导入包含新版源代码的仓库。若仓库根就是 hu-garden，Root Directory 使用默认值；若与旧版在同一仓库，选 hu-garden。Framework Preset 选择 Astro，构建命令 npm run build，输出目录 dist。将 SITE_URL 设置为站点真实公开源地址（含 https），BASE_PATH 保持空值。点击 Deploy，在发布结果中打开首页与文章深链。[Astro 的 Vercel 部署说明](https://docs.astro.build/en/guides/deploy/vercel/)

## 上线前清单

- [ ] 填写公开邮箱并测试邮件链接；复核昵称、文案和示例标签。
- [ ] 复核照片与音频授权、定位信息和文件名。
- [ ] npm ci 和 npm run build 成功，检查所有页面及嵌套路径。
- [ ] 在手机与桌面检查菜单、换行、触控、键盘焦点与减少动画设置。
- [ ] 测试灯箱关闭与焦点返回、手记搜索无结果、主题跨页保留。
- [ ] 首次打开保持静音，测试播放、暂停、切歌及音量。
- [ ] 验证 SITE_URL、网页分享图和更新日志。
- [ ] 在真实部署域名用无痕窗口打开深链，检查控制台、图片及音频请求。
