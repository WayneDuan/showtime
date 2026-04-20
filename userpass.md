# NowShowTime 用户指南

> 版本适用：当前最新版本

---

## 目录

1. [简介](#简介)
2. [界面总览](#界面总览)
3. [订阅源管理](#订阅源管理)
   - [JS 订阅源](#js-订阅源)
   - [Emby / Jellyfin 服务器](#emby--jellyfin-服务器)
   - [IPTV 直播源](#iptv-直播源)
   - [文件夹/网络存储](#文件夹网络存储)
   - [体验内容（无需订阅）](#体验内容无需订阅)
4. [站点管理](#站点管理)
5. [视频浏览](#视频浏览)
6. [视频详情与播放](#视频详情与播放)
7. [播放器操作](#播放器操作)
8. [全局搜索](#全局搜索)
9. [观看历史](#观看历史)
10. [设置](#设置)
11. [会员与解锁](#会员与解锁)
12. [常见问题](#常见问题)

---

## 简介

**NowShowTime** 是一款聚合式视频播放应用，支持将多种外部视频资源（JS 脚本订阅、Emby/Jellyfin 媒体服务器、IPTV 直播、网络存储等）统一管理并在一个界面内播放。

应用本身**不提供任何视频内容**，所有内容均来自用户自行添加的订阅源。

---

## 界面总览

应用底部共有四个标签页：

| 标签 | 功能说明 |
|------|----------|
| **首页** | 快速访问已选定的站点或精选内容 |
| **影视** | 浏览并管理所有订阅站点 |
| **搜索** | 跨站点全局搜索 |
| **设置** | 账号、播放、数据等配置 |

---

## 订阅源管理

在「**影视**」标签页，点击右上角 **+** 按钮，可添加以下类型的订阅源：

### JS 订阅源

通过一个 JSON 配置 URL 导入站点，每个 URL 可包含多个站点。

**添加步骤：**
1. 点击 **+** → **添加订阅**
2. 粘贴订阅 URL
3. 点击确认，应用自动拉取并解析

**管理订阅：**
- 进入「**设置 → 订阅管理**」
- 可单独刷新某条订阅，或一键刷新全部
- 支持清除某条订阅的 JS 脚本缓存
- 左滑订阅条目可删除

---

### Emby / Jellyfin 服务器

> 此功能为**会员专属**。

连接局域网或公网上的 Emby、Jellyfin 或 UHD 服务。

**添加步骤：**
1. 点击 **+** → **添加 Emby/Jellyfin**
2. 填写：
   - **名称**（自定义显示名）
   - **服务器地址**（IP 或域名）
   - **端口**（Emby 默认 8096，Jellyfin 默认 8096）
   - **用户名 / 密码**
3. 点击「**测试连接**」验证
4. 确认保存

**局域网自动发现：**
点击「扫描局域网」，应用会通过 mDNS 自动搜索本地网络中的 Emby/Jellyfin 服务器，点击结果即可快速填充地址信息。

---

### IPTV 直播源

支持标准 M3U / M3U8 格式的直播列表。

> 免费用户限添加 **1 个** IPTV 源；会员不限数量。

**添加步骤：**
1. 点击 **+** → **添加 IPTV 源**
2. 填写 M3U 地址
3. 可选：
   - **开启延迟检测** — 播放前 ping 每个频道，标注可用性
   - **开启频道预览** — 生成频道缩略图（耗费更多时间）
4. 点击「**测试**」验证源有效性后保存

**直播功能：**
- 同名频道自动合并，播放器内可切换多路线路
- 支持自定义 User-Agent

---

### 文件夹/网络存储

支持 SMB 共享、WebDAV 或本机本地文件夹。

1. 点击 **+** → **添加文件夹**
2. 填写网络路径（SMB/WebDAV）或选择本地目录
3. 保存后应用扫描目录内的视频文件

---

### 体验内容（无需订阅）

应用内置演示订阅，包含 Apple HLS 测试流和 Blender 开源电影，无需账号即可体验播放功能。

---

## 站点管理

在「**影视**」标签页，所有已订阅站点以网格形式展示。

### 筛选与搜索

顶部筛选栏可按类型过滤：
- **全部 / JS脚本 / Emby·Jellyfin / 直播 / 文件夹**

右上角搜索图标可按站点名称搜索。

### 排序与置顶

- **长按**站点图标进入快捷菜单：
  - **置顶 / 取消置顶** — 置顶的站点显示在最前
  - **隐藏站点** — 隐藏后不在主列表显示
  - **参与/不参与全局搜索** — 控制该站点是否出现在搜索结果中
  - **自定义图标** — 填入图片 URL 自定义站点图标
  - **删除站点**

- **编辑模式**（点击右上角铅笔图标）：
  - 长按站点图标拖拽**重新排序**
  - 点击站点角落按钮批量隐藏/删除

### 管理隐藏站点

进入编辑模式后，点击底部「显示隐藏站点」可查看并恢复已隐藏的站点。

---

## 视频浏览

点击任意站点进入视频列表页（`VideoListView`）：

### 分类切换

页面顶部为分类横向标签，点击切换分类。

### 排序

部分站点支持多种排序方式（最新、最热等），通过分类下方的分段控件切换。

### 搜索

点击右上角**搜索图标**，在当前站点内搜索视频标题。

### 视频列表

- 封面图 + 标题网格展示
- 支持下拉刷新
- 滚动到底部自动加载更多（分页）
- 顶部可能显示**精选轮播横幅**（最多 5 条）

### 快速直接播放

开启后点击封面图直接进入播放，跳过详情页。在站点设置或播放器设置中可调整此行为。

---

## 视频详情与播放

点击视频封面进入详情页：

- **封面大图** + 视频标题、简介、评分等元数据
- **分辨率 / 选集** 网格：选择画质或剧集
- **继续上次观看**：若有播放记录（>5 秒），显示进度提示；可选「从头播放」
- **相关推荐**（可在设置中关闭）

点击分辨率/选集按钮即开始播放。

---

## 播放器操作

### 基础控件

| 操作 | 说明 |
|------|------|
| 单击画面 | 显示 / 隐藏控制栏 |
| 播放/暂停按钮 | 控制播放 |
| 进度条 | 拖动跳转时间 |
| 倍速按钮 | 切换播放速度（0.25× ～ 2.0×） |
| 清晰度按钮 | 切换分辨率 |
| 选集按钮 | 切换剧集（连续剧） |
| 全屏按钮 | 切换全屏/竖屏 |

### 手势操作

所有手势可在「**设置 → 播放设置**」中单独开启或关闭，并调整灵敏度。

| 手势 | 默认行为 |
|------|----------|
| 左右滑动 | 快进 / 快退（可调整每10点对应秒数：5～30秒） |
| 左半屏上下滑动 | 调节**亮度** |
| 右半屏上下滑动 | 调节**音量** |
| 双击左侧 | 快退（可配置步长） |
| 双击右侧 | 快进（可配置步长） |

> 拖动进度时，屏幕上方会显示**绝对时间 + 偏移量**预览，松手后才实际跳转。

### 其他播放功能

- **循环播放**：单集循环
- **下载速度显示**：实时显示当前码率（KB/s 或 MB/s）
- **静音模式穿透**：即使手机静音，视频声音依然正常播放
- **自动记录进度**：关闭播放后自动保存位置，下次继续

---

## 全局搜索

在底部「**搜索**」标签页，可同时在多个站点中搜索视频。

### 使用方法

1. 在搜索框输入关键词，点击搜索
2. 应用并发请求各站点，实时显示各站点的结果
3. 点击结果条目进入对应视频详情

### 搜索设置

点击右上角齿轮图标进入搜索设置：

- **管理参与搜索的站点**：开启或关闭特定站点
- **并发数**（2～8）：同时搜索的站点数量。并发越高搜索越快，但对网络要求也更高

> IPTV 直播源和文件夹类型不参与全局搜索。

---

## 观看历史

进入「**设置 → 观看历史**」：

- 按时间倒序展示所有观看记录
- 每条记录显示：封面、标题、观看日期、**播放进度条**
- 点击条目可快速回到视频详情页并继续播放
- **左滑删除**单条记录
- 右上角「清除全部」可一键清空

> 会员开启 iCloud 同步后，观看历史会在多台设备间自动同步。

---

## 设置

「**设置**」标签页主要分以下几个区域：

### 账号与会员

- 查看当前会员状态（有效期、套餐类型）
- 购买或升级会员

### 播放设置

| 设置项 | 说明 |
|--------|------|
| 手势开关 | 分别控制左右滑动、上下滑动手势 |
| 左右滑动灵敏度 | 每10点像素对应的跳转秒数 |
| 双击步长 | 双击快进/快退的秒数 |
| 音量/亮度手势灵敏度 | 滑动调节的幅度 |
| 视频填充模式 | 等比适应 / 拉伸填满等 |
| 显示相关推荐 | 详情页是否显示推荐视频 |
| 循环播放 | 单视频循环 |
| 默认倍速 | 记住上次使用的播放速度 |

### 数据管理

- **订阅管理**：查看、刷新、删除订阅
- **观看历史**：查看及清除
- **iCloud 同步**（会员）：跨设备同步订阅和历史

### 语言

支持**简体中文**和**English**，切换后立即生效。

### 关于

- 版本号
- 社区：Telegram 频道 [@nshowtime](https://t.me/nshowtime) / 讨论组 [@nowshowtimechat](https://t.me/nowshowtimechat)
- 免责声明 / 开源许可证

---

## 会员与解锁

### 免费版限制

| 功能 | 免费 | 会员 |
|------|:----:|:----:|
| JS 订阅源 | 无限制 | 无限制 |
| IPTV 直播源 | 最多 1 个 | 无限制 |
| Emby / Jellyfin | — | ✓ |
| iCloud 同步 | — | ✓ |
| 高清/4K 解锁 | — | ✓ |
| 高级播放器设置 | ✓ | ✓ |
| 全局搜索 | ✓ | ✓ |
| 观看历史 | 本地 | 本地 + 云同步 |

### 会员套餐

- **月度会员**：按月自动续费
- **年度会员**：按年自动续费（推荐，性价比更高）
- **永久会员**：一次买断，长期使用

---

## 常见问题

**Q：视频无法播放，转圈不停**
- 检查网络连接
- 尝试切换其他分辨率
- 刷新订阅源（订阅管理 → 刷新）
- 清除该订阅的 JS 缓存后重试

**Q：部分站点显示"解析失败"或"降级模式"**
- 该站点的 JS 脚本可能已失效，需联系订阅提供方更新
- 尝试手动刷新订阅

**Q：Emby 服务器连接失败**
- 确认服务器地址、端口、账号密码无误
- 确认手机与服务器处于同一局域网（局域网连接场景）
- 检查服务器防火墙是否开放对应端口

**Q：IPTV 频道无法播放**
- 频道源可能已失效，请联系频道源提供方
- 尝试切换同频道的其他线路

**Q：如何让某站点不出现在全局搜索结果中？**
- 长按该站点图标 → 选择「不参与全局搜索」

**Q：iCloud 同步没有生效**
- 确认已开启会员
- 进入「设置 → iCloud 同步」检查开关状态
- 确认 iOS 设置中该应用的 iCloud Drive 权限已开启

**Q：如何联系官方？**
- Telegram 频道：[@nshowtime](https://t.me/nshowtime)
- Telegram 讨论组：[@nowshowtimechat](https://t.me/nowshowtimechat)

---

*文档由开发团队维护，如有功能更新以最新版应用为准。*

---

---

# NowShowTime User Guide

> Applies to: Current latest version

---

## Table of Contents

1. [Introduction](#introduction)
2. [App Overview](#app-overview)
3. [Managing Sources](#managing-sources)
   - [JS Subscriptions](#js-subscriptions)
   - [Emby / Jellyfin Servers](#emby--jellyfin-servers)
   - [IPTV Live Sources](#iptv-live-sources)
   - [Folder / Network Storage](#folder--network-storage)
   - [Demo Content (No Account Required)](#demo-content-no-account-required)
4. [Managing Sites](#managing-sites)
5. [Browsing Videos](#browsing-videos)
6. [Video Detail & Playback](#video-detail--playback)
7. [Player Controls](#player-controls)
8. [Global Search](#global-search)
9. [Watch History](#watch-history)
10. [Settings](#settings)
11. [Membership & Unlock](#membership--unlock)
12. [FAQ](#faq)

---

## Introduction

**NowShowTime** is an aggregated video player that lets you manage multiple external video sources — JS script subscriptions, Emby/Jellyfin media servers, IPTV live streams, and network storage — in a single interface.

The app **does not provide any video content itself**. All content comes from sources you add.

---

## App Overview

The app has four tabs at the bottom:

| Tab | Description |
|-----|-------------|
| **Home** | Quick access to a selected site or featured content |
| **Play** | Browse and manage all subscribed sites |
| **Search** | Cross-site global search |
| **Settings** | Account, playback, and data configuration |

---

## Managing Sources

In the **Play** tab, tap the **+** button in the top-right corner to add a source:

### JS Subscriptions

Import sites via a JSON configuration URL. A single URL can contain multiple sites.

**How to add:**
1. Tap **+** → **Add Subscription**
2. Paste the subscription URL
3. Tap confirm — the app fetches and parses it automatically

**Managing subscriptions:**
- Go to **Settings → Subscriptions**
- Refresh individual subscriptions or refresh all at once
- Clear the JS script cache for a specific subscription
- Swipe left on a subscription to delete it

---

### Emby / Jellyfin Servers

> This feature requires a **membership**.

Connect to Emby, Jellyfin, or UHD Service servers on your local network or the internet.

**How to add:**
1. Tap **+** → **Add Emby/Jellyfin**
2. Fill in:
   - **Name** (custom display name)
   - **Server address** (IP or domain)
   - **Port** (Emby/Jellyfin default: 8096)
   - **Username / Password**
3. Tap **Test Connection** to verify
4. Save

**LAN auto-discovery:**
Tap "Scan Local Network" — the app uses mDNS to automatically find nearby Emby/Jellyfin servers. Tap a result to auto-fill the address.

---

### IPTV Live Sources

Supports standard M3U / M3U8 playlist format.

> Free users can add **1 IPTV source**; members can add unlimited sources.

**How to add:**
1. Tap **+** → **Add IPTV Source**
2. Enter the M3U URL
3. Optional:
   - **Latency detection** — pings each channel before playback to indicate availability
   - **Channel preview** — generates channel thumbnails (takes longer)
4. Tap **Test** to validate, then save

**Live TV features:**
- Channels with the same name are merged; you can switch between multiple streams in the player
- Supports custom User-Agent per source

---

### Folder / Network Storage

Supports SMB shares, WebDAV, or local folders on the device.

1. Tap **+** → **Add Folder**
2. Enter the network path (SMB/WebDAV) or choose a local directory
3. After saving, the app scans the directory for video files

---

### Demo Content (No Account Required)

The app includes a built-in demo subscription with Apple HLS test streams and Blender open-source movies — no account needed to try playback.

---

## Managing Sites

In the **Play** tab, all subscribed sites are displayed in a grid.

### Filter & Search

Use the filter bar at the top to filter by type:
**All / JS Script / Emby·Jellyfin / Live TV / Folder**

Tap the search icon in the top-right to search by site name.

### Reorder & Pin

- **Long-press** a site icon to open the context menu:
  - **Pin / Unpin** — pinned sites appear at the top
  - **Hide Site** — removes it from the main list
  - **Include/Exclude from Global Search** — controls whether this site appears in search results
  - **Custom Icon** — enter an image URL for a custom site icon
  - **Delete Site**

- **Edit mode** (tap the pencil icon in the top-right):
  - Long-press and drag a site to **reorder**
  - Tap the corner button on a site to batch hide/delete

### Managing Hidden Sites

In edit mode, tap "Show Hidden Sites" at the bottom to view and restore hidden sites.

---

## Browsing Videos

Tap any site to open the video list:

### Categories

Category tabs are displayed horizontally at the top. Tap to filter by category.

### Sorting

Some sites support multiple sort options (Latest, Most Popular, etc.) via segmented controls below the categories.

### Search

Tap the **search icon** in the top-right to search video titles within the current site.

### Video List

- Grid layout with cover images and titles
- Pull down to refresh
- Scroll to the bottom to load more (pagination)
- A **featured banner carousel** (up to 5 items) may appear at the top

### Quick Direct Play

When enabled, tapping a cover image goes directly to playback, skipping the detail page. Adjust this in site or player settings.

---

## Video Detail & Playback

Tap a video cover to open the detail page:

- Large **cover image** with title, description, rating, and metadata
- **Resolution / Episode** grid — select quality or episode
- **Resume playback**: if a watch position exists (> 5 seconds), a resume prompt appears; tap "Start from Beginning" to reset
- **Related recommendations** (can be disabled in settings)

Tap a resolution or episode button to start playback.

---

## Player Controls

### Basic Controls

| Action | Description |
|--------|-------------|
| Single tap on screen | Show / hide controls |
| Play / Pause button | Toggle playback |
| Progress bar | Drag to seek |
| Speed button | Change playback speed (0.25× – 2.0×) |
| Quality button | Switch resolution |
| Episode button | Switch episode (for series) |
| Fullscreen button | Toggle fullscreen / portrait |

### Gesture Controls

All gestures can be individually enabled/disabled and adjusted in **Settings → Playback Settings**.

| Gesture | Default behavior |
|---------|-----------------|
| Swipe left / right | Seek backward / forward (5–30 s per 10 pts, configurable) |
| Swipe up / down on left half | Adjust **brightness** |
| Swipe up / down on right half | Adjust **volume** |
| Double-tap left side | Skip backward (configurable step) |
| Double-tap right side | Skip forward (configurable step) |

> While dragging the progress bar, a preview overlay shows the **absolute timestamp + offset**. The seek is committed only when you release.

### Other Playback Features

- **Loop playback** — repeat a single video
- **Download speed display** — real-time bitrate in KB/s or MB/s
- **Silent mode override** — audio plays even when the phone is on silent
- **Auto-save position** — progress is saved automatically; playback resumes next time

---

## Global Search

In the **Search** tab, you can search across multiple sites simultaneously.

### How to use

1. Enter a keyword in the search box and tap Search
2. The app queries all participating sites concurrently and shows results in real time
3. Tap a result to go to the video detail page

### Search Settings

Tap the gear icon in the top-right to open search settings:

- **Manage participating sites** — enable or disable individual sites
- **Concurrency** (2–8) — number of sites searched at the same time; higher concurrency is faster but requires better network

> IPTV live sources and folder libraries are excluded from global search.

---

## Watch History

Go to **Settings → Watch History**:

- All watched videos listed in reverse chronological order
- Each entry shows: cover thumbnail, title, watch date, and a **playback progress bar**
- Tap an entry to return to the video detail page and resume
- **Swipe left** to delete a single entry
- Tap "Clear All" in the top-right to remove everything

> Members with iCloud Sync enabled will have watch history automatically synced across all devices.

---

## Settings

The **Settings** tab is organized into the following sections:

### Account & Membership

- View current membership status (expiry date, plan type)
- Purchase or upgrade membership

### Playback Settings

| Setting | Description |
|---------|-------------|
| Gesture toggles | Enable/disable horizontal and vertical swipe gestures individually |
| Horizontal sensitivity | Seconds to seek per 10 points of swipe distance |
| Double-tap step | Seconds to skip per double-tap |
| Volume/brightness sensitivity | Sensitivity for swipe-to-adjust gestures |
| Video fill mode | Aspect fit, aspect fill, stretch, etc. |
| Show recommendations | Display related videos on the detail page |
| Loop playback | Repeat a single video |
| Default speed | Remember the last-used playback speed |

### Data Management

- **Subscriptions** — view, refresh, or delete subscriptions
- **Watch History** — browse and clear
- **iCloud Sync** (members only) — sync subscriptions and history across devices

### Language

Supports **English** and **简体中文 (Simplified Chinese)**. Takes effect immediately after switching.

### About

- Version number
- Community: Telegram channel [@nshowtime](https://t.me/nshowtime) / discussion group [@nowshowtimechat](https://t.me/nowshowtimechat)
- Disclaimer / Open-source licenses

---

## Membership & Unlock

### Free vs. Member

| Feature | Free | Member |
|---------|:----:|:------:|
| JS Subscriptions | Unlimited | Unlimited |
| IPTV Sources | 1 | Unlimited |
| Emby / Jellyfin | — | ✓ |
| iCloud Sync | — | ✓ |
| HD / 4K Quality | — | ✓ |
| Advanced Player Settings | ✓ | ✓ |
| Global Search | ✓ | ✓ |
| Watch History | Local only | Local + cloud sync |

### Membership Plans

- **Monthly** — recurring monthly subscription
- **Yearly** — recurring yearly subscription (recommended, better value)
- **Lifetime** — one-time purchase, permanent access

---

## FAQ

**Q: Video won't play / keeps buffering**
- Check your network connection
- Try switching to a different resolution
- Refresh the subscription (Subscriptions → Refresh)
- Clear the JS cache for that subscription and try again

**Q: A site shows "parse failed" or "fallback mode"**
- The site's JS script may be outdated — contact the subscription provider for an update
- Try refreshing the subscription manually

**Q: Emby server connection failed**
- Double-check the server address, port, username, and password
- Make sure your phone and server are on the same local network (for LAN connections)
- Check that the server's firewall allows traffic on the configured port

**Q: IPTV channel won't play**
- The channel stream may have expired — contact your IPTV source provider
- Try switching to a different stream route for the same channel in the player

**Q: How do I exclude a site from global search?**
- Long-press the site icon → select "Exclude from Global Search"

**Q: iCloud Sync isn't working**
- Confirm your membership is active
- Go to Settings → iCloud Sync and check the toggle
- In iOS Settings, make sure iCloud Drive access is enabled for this app

**Q: How do I contact support?**
- Telegram channel: [@nshowtime](https://t.me/nshowtime)
- Telegram discussion group: [@nowshowtimechat](https://t.me/nowshowtimechat)

---

*This document is maintained by the development team. Refer to the latest app version for the most up-to-date features.*
