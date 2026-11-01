# 手帐本（iOS 版）

iPad + Apple Pencil 的手帐本。PencilKit 原生接笔：压感、防误触、工具栏。iPhone 上手指也能画、能贴贴纸、能打字。

- 不联网，不统计，不收集任何数据。本子只存在本机，没有云同步。
- 不用 Mac，不用付费开发者账号。用免费 Apple ID + AltStore 侧载，7 天续签一次。

## 结构：先分类，再贴纸

风格（主题）决定整本的纸、颜色、默认字体和封面：

- **复古**：哥特、推理、College
- **可爱**：日系、宠物
- **时尚**：空壳子，贴纸以后再加

贴纸是清单驱动的：`JournalApp/Resources/stickers.json` 里写分类和文件名。以后加贴纸，只需要往 `Resources/Stickers/` 里加 PNG，再在清单里加一行，不用改代码。

### 首批贴纸（4 张）

| 贴纸 | 分类 |
|---|---|
| 黑玫瑰 | 复古 / 哥特 |
| 水彩玫瑰、草莓蛋糕 | 可爱 / 日系 |
| 三花猫 | 可爱 / 宠物 |

**老实说一句：这 4 张贴纸底色是不透明的白色**（生成时要求了透明底，实际到手的是 RGB 无 alpha 通道，边角取样全是纯白）。打包时照原样打进去了，贴在纸上会是一块白色方底，不是透明异形。如果以后重新切了透明底，直接替换同名 PNG 即可，不用改代码。

### 封面

- **复古封面**：打包了（绿皮烫金黑玫瑰那张）。
- **可爱封面**：被否了，没有打包。可爱风格的本子先用**纯色占位封面**，新封面定稿后再换。换封面只需要把新图放进 `Resources/Covers/` 并在设置里可选，不用改代码（目前封面选项只有“复古封面”和“纯色占位”）。
- 应用图标用的是复古封面中央黑玫瑰的方形裁切。

### 字体（都打包了，OFL 开源协议）

马善政书法、芝芒行书、龙藏体、Great Vibes、Dancing Script、Caveat。字体名都实测过能从文件里读出来。万一某个字体在真机上加载失败，代码里有兜底：自动回系统字体，不会崩。

## 玩法

- 书架：新建本子（选风格、选封面），点封面打开，长按（或右键菜单）改设置、删本子。
- 画笔模式：Apple Pencil 直接画，工具栏选笔和颜色；“仅用笔”开关打开后手指不画画，只画笔能画，防手掌误触。关掉后手指也能画。
- 排版模式：贴纸拖动、双指缩放、旋转、删除；文字框拖动、点开改字、换字体、大小、颜色；贴纸可以在墨水上层或下层。
- 纸：每页可以换纸色（按风格给 3 种）；加页、删页、上一页、下一页。
- 导出：把当前页导出成 PNG 图片，用系统分享单发出去。
- 保存：所有修改自动存到本机 Documents，重新打开都在。

## 需要什么

- 一个 GitHub 账号（免费）
- 一台 Windows 电脑（装 AltServer）
- 一台 iPad（iPadOS 17 或更新）+ Apple Pencil；iPhone 也能装，手指画
- 一个 Apple ID（免费账号就行，密码只输在 AltStore / AltServer 里，绝不进仓库）

## 第一步：把代码传到 GitHub（公开仓库）

仓库必须是**公开（Public）**的，GitHub 免费的 macOS 构建机只给公开仓库免费用。

网页上传（不用装任何东西，推荐）：

1. 打开 github.com，点右上角 `+` → `New repository`。
2. Repository name 填 `pocket-journal`，选 **Public**，点 `Create repository`。
3. 点 `uploading an existing file`，把本项目文件夹里的**全部内容**拖进去（包括 `.github` 文件夹和 `.gitignore`），点 `Commit changes`。

备选：电脑上有 git 的话，在项目文件夹里跑：

```bash
git init
git add .
git commit -m "Journal"
git branch -M main
git remote add origin https://github.com/<你的用户名>/pocket-journal.git
git push -u origin main
```

## 第二步：云端构建，拿到 .ipa

1. 打开仓库页面，点顶部的 **Actions**。
2. 左边点 `Build unsigned IPA`，点右边的 **Run workflow** → **Run workflow**。
3. 等跑完（几分钟）。绿色对勾 = 成功。
4. 点那次运行记录，拉到最下面 **Artifacts**，下载 `Journal-unsigned`，解压得到 `Journal.ipa`。
5. 构建失败（红色叉）先看后面的“常见问题”第 1 条，不要反复点运行。

## 第三步：电脑装 AltServer

1. 先装苹果官网版的 **iTunes** 和 **iCloud**（从 apple.com/support 下载）。
   **不要用微软商店版**，商店版 AltServer 认不出设备。这是 AltStore 官方文档的要求。
2. iCloud 打开登录一次你的 Apple ID。
3. 从 [altstore.io](https://altstore.io) 下载 AltServer（Windows 版），安装，运行。
   任务栏会出现一个菱形图标。点它 → `Install AltStore` 时再看下一步。

## 第四步：iPad 装 AltStore

1. iPad 用数据线连电脑，解锁，点“信任此电脑”。
2. 电脑任务栏点 AltServer 图标 → `Install AltStore` → 选你的 iPad。
3. 提示输入 Apple ID 和密码：只发给苹果验证，输完即可。开了双重认证按提示输验证码。
4. iPad 上打开 AltStore，会提示“未受信任的开发者”：
   设置 → 通用 → VPN 与设备管理 → 点你的 Apple ID → **信任**。
5. 打开 **开发者模式**（iPadOS 16 及以上需要）：
   设置 → 隐私与安全 → 开发者模式 → 打开 → 重启 → 弹窗点“打开”。
   如果列表里找不到这个开关：先装一次应用并点开它，系统弹过提示后开关才会出现。

## 第五步：装手帐本

1. 把 `Journal.ipa` 传到 iPad（微信文件传输助手、或直接在 iPad 浏览器里从 GitHub 下载都行，文件要落在“文件”App 里）。
2. 打开 AltStore → 底部 **My Apps** → 左上角 `+` → 选 `Journal.ipa`。
3. 按提示输入 Apple ID，等待安装完成。主屏幕出现“手帐本”图标。
4. 第一次打开如果提示未受信任，按第四步第 4 条信任一次即可。

## 第六步：7 天续签

免费 Apple ID 签的证书 7 天过期，过期后应用打不开，需要重新签：

- 电脑开着 AltServer，iPad 和电脑连**同一个 Wi-Fi**，AltStore 会自动续签。
- 也可以手动：AltStore → My Apps → 应用旁边的剩余天数 → 点刷新。
- 免费账号最多同时装 3 个自己签的应用，AltStore 自己占 1 个名额。名额满了先删不用的。

## 常见问题

1. **Actions 构建失败（红色叉）**
   点进那次运行，看第一个红色的步骤日志。最常见的原因是 Xcode 路径变了：工作流里写的是 `/Applications/Xcode_26.3.app`，如果 GitHub 换了镜像，日志里会报找不到。修法：改 `.github/workflows/ios.yml` 里那一行，改成日志中实际存在的版本（先在日志里搜 `Xcode_` 看有哪些）。不要改别的。
2. **AltServer 找不到设备**
   八成是 iTunes 装了微软商店版。卸载商店版，装苹果官网版 iTunes + iCloud，重启电脑，重新插线。
3. **“未受信任的开发者”**
   设置 → 通用 → VPN 与设备管理 → 点 Apple ID → 信任。每次重签后可能要重新信任一次。
4. **找不到“开发者模式”开关**
   先装一次应用并点开它，系统弹过一次提示后，开关才会出现在“设置 → 隐私与安全”最下面。
5. **7 天后应用打不开**
   证书过期了。电脑开 AltServer + 同 Wi-Fi，让 AltStore 自动续签；或删了重装。
6. **AltStore 提示应用数量超限**
   免费账号最多 3 个，AltStore 占 1 个。删掉不用的侧载应用再装。
7. **构建日志报证书 / 签名错误**
   工作流是无签名的（`CODE_SIGNING_ALLOWED=NO`），正常情况下不该报签名错。如果报了，把日志原样发来，不要自己往仓库里加任何证书、密码、Apple ID。

## 没验证的，老实说

- 这里没有 Mac、没有 iPad、没有 Apple Pencil，这套流程**没有实际跑通过**。第一次云端构建可能失败，修法在日志里，不保证一次成功。
- Xcode 26.3 的路径是 2026-11-01 按 GitHub 官方镜像文档核实的（macos-15 镜像带 26.0.1/26.1.1/26.2/26.3，默认是 16.4），镜像更新后可能漂移，见常见问题第 1 条。
- PencilKit 在真笔上的压感、掌心防误触、工具栏表现，没有在真机上验过；以 iPad 上实际体验为准。
- 墨水坐标按画布尺寸存，换尺寸很大的设备打开同一页时墨水位置可能对不上——v1 的已知限制，本机常用设备上没问题。
- AltStore 的界面文字可能随版本变化，步骤意思不变，按钮位置以你设备上实际看到的为准。
- 代码是按 Swift 6 / iOS 17 写的，没有在真机 Xcode 里编译过，第一次构建就是编译检查。

## 项目结构

```
project.yml                  XcodeGen 工程定义（单 target，无签名）
JournalApp/
  JournalApp.swift           入口
  Models.swift               主题、字体、数据模型（本子/页/贴纸/文字）
  JournalStore.swift         清单加载 + 本子存取（本机 Documents）
  CanvasView.swift           PencilKit 画布封装 + 工具栏
  PageEditorView.swift       编辑器：纸、墨水、贴纸、文字、工具栏、导出
  StickerPickerView.swift    贴纸选择器（风格 → 分类 → 贴纸）
  ShelfView.swift            书架、封面、建本子、改设置
  Exporter.swift             页面导出 PNG + 分享单
  Assets.xcassets/           只有 AppIcon（由复古封面裁切生成全尺寸）
  Resources/
    stickers.json            贴纸清单（分类驱动）
    Stickers/                4 张首批贴纸（白底不透明，见上）
    Covers/                  cover-vintage.jpg（可爱封面被否，未打包）
    Fonts/                   6 个 OFL 字体
.github/workflows/ios.yml    云端无签名构建，产出 Journal.ipa
```

Bundle ID：`com.meowmiya.journal`，显示名：手帐本，iOS 17+，iPhone 竖屏、iPad 全方向。
