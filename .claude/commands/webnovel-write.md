---
allowed-tools: Read, Write, Edit, Grep, Bash
argument-hint: [章节号]
description: 按大纲创作指定章节的正文内容（3000-5000字），自动进行三大定律检查和爽点规划
---

# /webnovel-write

按大纲创作章节正文，严格遵守防幻觉三大定律。

## 执行流程

1. **读取章节大纲** - 从 `大纲/` 找到对应章节
2. **读取上下文** - 前 3 章 + 主角卡 + 相关设定
3. **调用 webnovel-writer skill**（创作模式）
4. **质量检查** - 大纲符合度/设定一致性/爽点密度
5. **保存章节** - 写入 `正文/第XXXX章.md`
6. **更新状态** - 更新 state.json 进度
7. **自动备份** - 执行 Git 提交（原子性版本控制）
   ```bash
   python scripts/backup_manager.py --chapter {章节号} --chapter-title "{章节标题}"
   ```
8. **检查审查节点** - 每 10 章触发自动审查

## 使用示例

```
/webnovel-write 1      # 创作第 1 章
/webnovel-write 45     # 创作第 45 章
```

## 输出

生成的章节文件包含：
- 正文内容（3000-5000 字）
- 本章统计（字数/爽点/新角色/伏笔）
- [NEW_ENTITY] 标签（如有）
