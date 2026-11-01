# AltStore 安装清单（iPad）

装“手帐本”之前，先拿到 `Journal.ipa`（见 README 第二步：GitHub Actions 构建产物）。

## 电脑端（Windows）

- [ ] 装苹果官网版 **iTunes**（apple.com/support 下载，**不要微软商店版**）
- [ ] 装苹果官网版 **iCloud**，打开登录一次 Apple ID
- [ ] 从 [altstore.io](https://altstore.io) 下载 **AltServer**（Windows 版），安装并运行（任务栏出现菱形图标）

## iPad 端装 AltStore

- [ ] iPad 数据线连电脑，解锁，点“信任此电脑”
- [ ] 电脑任务栏点 AltServer 图标 → `Install AltStore` → 选你的 iPad
- [ ] 输入 Apple ID 和密码（只发给苹果验证；双重认证按提示输验证码）
- [ ] iPad 上打开 AltStore，提示未受信任时：设置 → 通用 → VPN 与设备管理 → 点 Apple ID → **信任**
- [ ] 开开发者模式：设置 → 隐私与安全 → 开发者模式 → 打开 → 重启 → 弹窗点“打开”
  （找不到开关：先装一次应用并点开它，弹过提示后开关才会出现）

## 装手帐本

- [ ] 把 `Journal.ipa` 传到 iPad“文件”App（微信文件传输助手 / 浏览器下载都行）
- [ ] 打开 AltStore → **My Apps** → 左上角 `+` → 选 `Journal.ipa`
- [ ] 按提示输入 Apple ID，等安装完成，主屏幕出现“手帐本”

## 7 天续签（免费 Apple ID）

- [ ] 电脑开着 AltServer，iPad 和电脑连**同一个 Wi-Fi**，AltStore 自动续签
- [ ] 或手动：AltStore → My Apps → 剩余天数 → 点刷新
- [ ] 免费账号最多 3 个侧载应用，AltStore 自己占 1 个

## 出问题先查

- AltServer 找不到设备 → 八成是微软商店版 iTunes，换苹果官网版
- “未受信任的开发者” → 设置 → 通用 → VPN 与设备管理 → 信任
- 7 天后打不开 → 证书过期，续签或重装
- 提示数量超限 → 删不用的侧载应用
