# Task Sync

TickTick <-> Google Tasks 双向实时同步

## 日期策略（防止 Google Calendar 重复）

| 列表类型 | 日期 | 说明 |
|----------|------|------|
| 常规列表 | ❌ 不含日期 | 日期转发到 TickTick 后从 Google 清除 |
| All 智能列表 | ✅ 含日期 | Calendar 唯一数据源 |
| Today / Next 7 Days | ❌ 不含日期 | 仅作为过滤视图 |

## 同步流程

1. **列表同步**（双向）：Google Lists <-> TickTick Projects 自动匹配/创建
2. **任务同步**（双向）：标题、完成状态、优先级（TickTick 优先级 -> Google 标题前缀）
3. **智能列表**（单向 TickTick -> Google）：Today、Next 7 Days、All

## 文件结构

| 文件 | 说明 |
|------|------|
| `sync.py` | 主同步脚本 |
| `utils/google_api.py` | Google Tasks API（支持分页、Token 自动刷新） |
| `utils/ticktick_api.py` | TickTick Open API 封装 |
| `scripts/setup_ticktick.py` | TickTick OAuth 授权 |
| `scripts/setup_google_tasks.py` | Google Tasks 权限设置 |
| `config.json` | 配置文件 |

## 数据文件

| 文件 | 说明 |
|------|------|
| `sync_db.json` | 任务映射数据库 |
| `sync_log.json` | 同步统计日志 |
| `data/ticktick_token.json` | TickTick Access Token |

## 使用

```bash
# 手动同步
/home/ubuntu/.openclaw/workspace/task-sync/sync.py

# 查看日志
cat /home/ubuntu/.openclaw/workspace/task-sync/sync_log.json
```

## Cron

每 10 分钟自动同步（通过 OpenClaw cron 系统）
