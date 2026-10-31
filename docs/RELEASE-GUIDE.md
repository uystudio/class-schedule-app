# 营职课表 · 新版发布指南

> 这份指南是给你自己看的操作说明书：以后每发一个新版 App，照着这里做就行。

---

## 一、新版 App 在哪里发布？

**发布地点：GitHub 仓库 `uystudio/class-schedule-app`**（就是你现在的下载站，没有第二个地方）。

发布之后，下载站网址**永远不变**：

**https://uystudio.github.io/class-schedule-app/**

发完新版，同学打开的还是这个网址，里面自动变成新版，不用换链接。

---

## 二、为什么"发布"这么简单？（大白话原理）

下载站的所有文件都放在这个 GitHub 仓库里：

- APK 文件放在 `docs/apk/` 文件夹
- 下载页文字放在 `docs/index.html`

你只要做三件事：**放进新 APK → 改一下页面文字 → 推送上去**。

推上去之后，GitHub 会自动重新生成下载站（大概 2~3 分钟），下载页自动变成新版。

所以：**发布新版 = 更新这个仓库，下载站自动跟上**。这就是"联通"。

---

## 三、发布新版要准备什么

1. **新版 APK 文件**（建议文件名用 `yingzhi-timetable-v1.0.69.apk` 这种英文格式，别用中文名）
2. **电脑**（就是你现在这台，GitHub 已经登录配置好了）

---

## 四、方式一：让豆包帮你发（推荐，最省事）

1. 把新版 APK 文件拖进豆包聊天窗口，发给我
2. 说一句：**"发布新版 App"**
3. 我来帮你一条龙搞定：
   - 算出新 APK 的 SHA-256 校验值
   - 把 APK 放进仓库 `docs/apk/`
   - 更新下载页里的版本号、文件名、大小、校验值
   - 推送上去
   - 等部署完成后验证下载站能下到新版
   - 最后告诉你：可以发给同学了

整个过程你不用碰命令行，也不用手动改页面。

---

## 五、方式二：自己用命令行发（想学可以照这个来）

打开电脑的 **PowerShell**（开始菜单搜"PowerShell"），逐条复制粘贴执行：

**第 1 步：把新版 APK 复制进仓库**

```powershell
Copy-Item "新版APK的完整路径" -Destination "C:\Users\Administrator\Documents\deepseek-harness\default-workspace\class-schedule-app\docs\apk\yingzhi-timetable-v1.0.69.apk"
```

（把 `新版APK的完整路径` 换成你新版 APK 实际的位置，比如 `C:\Users\Administrator\Desktop\营职课表-安装包-v1.0.69.apk`）

**第 2 步：算新版 APK 的 SHA-256（填页面校验区用）**

```powershell
Get-FileHash "C:\Users\Administrator\Documents\deepseek-harness\default-workspace\class-schedule-app\docs\apk\yingzhi-timetable-v1.0.69.apk" -Algorithm SHA256
```

记下输出的那一长串字母数字。

**第 3 步：改下载页文字**

用记事本打开：

```
C:\Users\Administrator\Documents\deepseek-harness\default-workspace\class-schedule-app\docs\index.html
```

按 `Ctrl + H` 逐个替换（把 68 换成 69 对应的内容）：

| 替换什么 | 替换成什么 |
| --- | --- |
| v1.0.68 | v1.0.69 |
| yingzhi-timetable-v1.0.68.apk | yingzhi-timetable-v1.0.69.apk |
| 51.5 MB | 新版的实际大小 |
| 54,054,962 字节 | 新版的实际字节数 |
| E8413A92...（SHA-256） | 第 2 步算出来的新校验值 |

（大小和字节数：在仓库文件夹里右键 APK → 属性 → 查看"大小"）

**第 4 步：推送**

```powershell
cd C:\Users\Administrator\Documents\deepseek-harness\default-workspace\class-schedule-app
git add docs
git commit -m "发布 v1.0.69"
git push origin main
```

**第 5 步：等 2~3 分钟，打开下载站网址验证**

https://uystudio.github.io/class-schedule-app/

确认页面上是 v1.0.69、大小和校验值都对，点「下载安装包」能下到新版。

---

## 六、注意事项

1. **APK 超过 50MB 会有一条黄色提醒**："File is larger than 50MB"——这只是提醒，不是错误，照常能发布（现在 51.5MB 的 v1.0.68 就是这么发的）。
2. **刚推完别立刻看页面**：GitHub 要 2~3 分钟重新生成下载站，太快会看到旧版，等一会儿刷新就好。
3. **下载站网址永远不变**：https://uystudio.github.io/class-schedule-app/
4. **SHA-256 不能填错**：校验值写错，同学装了会以为文件损坏。拿不准就直接走"方式一"让豆包帮你算。
5. **发布指南和下载站在同一个仓库**：打开仓库 https://github.com/uystudio/class-schedule-app 就能看到这份指南，随时回来查。

---

*当前已发布版本：v1.0.68（2026-10-31 部署）*
