# CMX Reader

一款专为 **CMX** 漫画格式打造的专业 Web 端阅读器，纯前端实现，无需安装任何软件，直接在浏览器中即可流畅阅读。

[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE)   [![CMXReader Version](https://img.shields.io/badge/CMX_Reader-1.0.0-blue.svg)](cmx-reader.html)   [![CMX](https://img.shields.io/badge/spec-CMX_1.0-informational.svg)](cmx-reader.html)

---

## 功能特性

- **CMX 格式原生支持** — 专为 CMX v1.0 格式优化，支持 O(1) 随机页面访问
- **AES-256-GCM 加密** — 支持加密文件的解密阅读，密码保护漫画内容
- **内置缩略图** — 侧边栏缩略图导航，快速跳转任意页面
- **双页模式** — 支持单页/双页阅读模式切换
- **RTL 模式** — 支持从右到左（日漫）阅读方向
- **缩放控制** — 鼠标滚轮/键盘快捷键自由缩放
- **沉浸式阅读** — 全屏/沉浸式模式，无干扰阅读体验
- **内置转换器** — 将 ZIP / CBZ / 图片文件夹转换为 CMX 格式（Web版仅支持 ZIP / CBZ 格式, Python版支持所有格式）
- **拖拽打开** — 拖拽 .cmx 文件到窗口即可打开
- **文件信息查看** — 查看 CMX 文件详细信息与完整性校验（MD5）
- **纯前端实现** — 无需后端，所有数据在本地处理，保护隐私

## 快速开始

### 方式一：直接打开

1. 下载 [cmx-reader.html](index.html)
2. 用浏览器直接打开即可使用

### 方式二：本地服务器

```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .
```

然后在浏览器中访问 `http://localhost:8080/cmx-reader.html`

### 方式三：github-pages 体验
1. 点击 [cmx-reader]([index.html](https://loongkc.github.io/CMX-Reader/))
2. 直接在浏览器打开即可使用体验

**注：github-pages加载文件等会慢很多，仅作为功能体验使用，不能代表本地运行性能**

## 使用方法

### 打开 CMX 文件

- 点击工具栏的 **📂 打开 CMX 文件** 按钮
- 或将 `.cmx` 文件 **拖拽** 到阅读器窗口中

### 阅读模式

| 模式 | 说明 |
|------|------|
| 单页模式 | 每次显示一页，适合大多数场景 |
| 双页模式 | 每次显示两页（跨页展开），适合宽屏显示器 |
| RTL 模式 | 从右到左阅读，适合日漫 |

### 缩略图导航

点击工具栏的缩略图按钮打开侧边栏，点击任意缩略图即可跳转到对应页面。

### 文件信息

按 `Ctrl + I` 或点击工具栏信息按钮，可查看：
- 文件基本信息（页数、大小、版本）
- 压缩与加密状态
- MD5 完整性校验

### 内置转换器

点击工具栏的 **🔄 转换器** 按钮，可以将以下源文件转换为 CMX 格式：

- `.zip` / `.cbz` 文件
- 图片文件（支持多选）
- 图片文件夹

转换器支持设置标题和密码加密（AES-256-GCM）。

## 快捷键

| 快捷键 | 功能 |
|--------|------|
| `←` / `↑` / `PageUp` | 上一页 |
| `→` / `↓` / `PageDown` / `空格` | 下一页 |
| `Home` | 跳到第一页 |
| `End` | 跳到最后一页 |
| `+` / `=` | 放大 |
| `-` | 缩小 |
| `0` | 重置缩放 |
| `F` | 切换沉浸式模式 |
| `Ctrl + O` | 打开文件 |
| `Ctrl + D` | 切换双页模式 |
| `Ctrl + R` | 切换 RTL 方向 |
| `Ctrl + I` | 查看文件信息 |
| `Esc` | 关闭弹窗 / 退出沉浸模式 |

> 快捷键需要在设置中开启「启用键盘快捷键」选项。

## 设置面板

点击工具栏的设置按钮打开设置面板，可配置：

- **阅读方向** — LTR（从左到右）/ RTL（从右到左）
- **阅读模式** — 单页 / 双页
- **缩放** — 滑块调整默认缩放比例
- **键盘快捷键** — 启用/禁用快捷键
- **关于** — 查看版本信息与功能介绍

## 技术栈

- **纯 HTML / CSS / JavaScript** — 单文件实现，零依赖构建
- **pako** — zlib 压缩/解压引擎
- **JSZip** — ZIP 文件读取（转换器）
- **Web Crypto API** — AES-256-GCM 加密/解密
- **PBKDF2** — 密钥派生函数

## 关于 CMX 格式

**CMX（Comic Manga eXtended Format）** 是一种专为漫画设计的二进制文件格式，相比传统的 CBZ/ZIP 格式具有以下优势：

| 特性 | CBZ/ZIP | CMX |
|------|---------|-----|
| O(1) 随机访问 | ❌ 需遍历 | ✅ 固定索引，直接跳转 |
| 内置缩略图 | ❌ | ✅ 快速预览 |
| 原生加密 | ❌ | ✅ AES-256-GCM |
| 漫画元数据 | ❌ | ✅ JSON 元数据 |
| 内容校验 | ❌ | ✅ MD5 完整性校验 |
| 流式加载 | ❌ | ✅ 支持 HTTP Range |

### 文件结构

```
┌─────────────────────────────────┐
│       FILE HEADER (64B)         │  魔数 + 版本 + 全局信息
├─────────────────────────────────┤
│       METADATA BLOCK            │  JSON 漫画元数据
├─────────────────────────────────┤
│       PAGE INDEX TABLE          │  固定步长页索引（48B/条）
├─────────────────────────────────┤
│       THUMBNAIL STRIP           │  所有页缩略图
├─────────────────────────────────┤
│       IMAGE DATA POOL           │  页面图像数据（压缩/加密）
├─────────────────────────────────┤
│       FOOTER + CHECKSUM (32B)   │  文件完整性校验
└─────────────────────────────────┘
```

> 完整格式规范请参阅 [CMX_SPEC.md](CMX_SPEC.md)

## 系统要求

- 现代浏览器（Chrome / Edge / Firefox / Safari 最新版）
- 支持 Web Crypto API
- 无需任何服务器环境

## 项目结构

```
cmx/
├── CMX_SPEC.md          # CMX 格式规范文档
├── cmx_format.py        # CMX格式标准
├── cmx_engine.py        # Python 工具库（编码/解码/转换）
├── cmx_gui.py           # 转换器界面（调用engine，全格式支持）
├── cmx_reader.py        # CMX 阅读器（主程序）
├── index.html           # CMX 阅读器（cmx-reader.html, Web迁移版）
└── README.md
```

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

[MIT License](LICENSE)

## 免责声明

本工具仅供学习和个人使用。请尊重版权，不要用于传播侵权内容。
