# Sweet Connect (enhanced)

Sweet Connect 2.3.8 (SA-MP 0.3.7 R1) 的**增强补丁版**。
本仓库只包含修改后的主脚本，保持最小改动、便于与官方版本对照。

## 原版

- 官方帖子：<https://www.blast.hk/threads/48078/>
- 请先按官方方式安装原版 Sweet Connect（含其 `moonloader/lib` 依赖）。

## 安装

1. 安装官方 Sweet Connect 2.3.8（确保其 `moonloader/lib` 依赖就位）。
2. 用本仓库的 `Sweet Connect.lua` 覆盖
   `<GTA根>\moonloader\Sweet Connect.lua`。

## 增强内容

- **修复 `/sc` 软重连出生崩溃。**
  根因：samp.dll 内部一个 append 表（base `0x136B38`，元素 20 字节，
  “下一写入下标”计数器 `0x13B958`）在软重连时不重置，跨会话累积；
  下标到 1027 时越界写脏对象池指针 `0x13BB74`，出生即崩。
  修复：在软重连切到 `WAIT_CONNECT` 前把该下标重置为 0，等同冷启动状态。

冷启动进服、普通死亡重生本就正常；该补丁只影响 `/sc` 软重连路径。
