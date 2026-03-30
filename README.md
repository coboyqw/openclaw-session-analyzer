# OpenClaw Session Analyzer

分析 OpenClaw 钱包创建会话，输出**可视化 Markdown 报告**，通过 Mermaid 图表和详细时间线表格，一眼看出耗时瓶颈（>10s标红）。

## 核心功能

- **三个核心指标**: A（端到端）、B（排除思考）、C（思考时间）
- **B值细分**: 区分 `B_tech`（技术耗时）和 `B_human`（用户等待）
- **可视化图表**: 甘特图、时序图、Top N 耗时排行
- **智能截止点**: 自动识别 `wallet_active` / `status: active`

## 快速开始

### 1. 安装技能

将 `skills/openclaw-session-analyzer/SKILL.md` 发送给 OpenClaw Agent，或安装到技能库：

```bash
# 如果是 OpenClaw 环境
请按「OpenClaw Session Analyzer」技能分析本场对话
```

### 2. 使用方式

**方式A - 自动查找最新会话（推荐）**:
```
请分析本场钱包创建会话的耗时
```

**方式B - 手动指定文件**:
```
请分析会话文件: ~/.openclaw/agents/main/sessions/xxx.jsonl
```

### 3. 查看报告

报告输出到: `/root/.openclaw/workspace/session_<UUID>_analysis.md`

## 报告内容

### 执行摘要
```
A（端到端）:       221.3秒
B（排除思考）:     79秒
  ├─ B_tech（技术）: 18秒   ← 技术优化目标
  └─ B_human（用户）: 143秒  ← 交互等待
C（思考时间）:     142.3秒
Cobo_exec:         6.7秒
```

### 可视化图表
- **甘特图**: 时间线视觉化，>10s标红
- **时序图**: 调用关系与时间标注
- **Top N 排行**: 一眼看出瓶颈

### 关键优化建议
- 使用 `--non-interactive` 模式消除用户等待
- 预安装 Skill + TSS 减少 bootstrap 时间
- 并行下载与后台任务优化

## 文件说明

| 文件 | 说明 |
|------|------|
| `skills/openclaw-session-analyzer/SKILL.md` | 核心技能文件（366行），包含完整分析规范 |
| `README.md` | 本文件，使用教程 |

## 常见问题

**Q: 需要我提供 session 路径吗？**  
A: 不需要，Agent 会自动到 `~/.openclaw/agents/main/sessions/` 查找。

**Q: 什么时候使用？**  
A: 建议**对话结束后**（钱包创建完成）再执行分析。

**Q: 报告时间是什么时区？**  
A: 使用 JSON 原始 **ISO 8601 UTC 时间**，不换算时区。

**Q: 如何分享报告给 Telegram 用户？**  
A: 报告保存在 `/root/.openclaw/workspace/`，可直接发送 `.md` 文件或复制内容。

## 贡献

欢迎提交 Issue 和 PR 改进此技能。

## License

MIT
