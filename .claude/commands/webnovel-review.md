---
allowed-tools: Read, Bash
argument-hint: [起始章-结束章]
description: 对指定范围的章节进行质量审查，调用 5 个专职审查员生成报告
---

# /webnovel-review

质量审查，调用 5 个审查员（agents）生成综合报告。

## 审查员团队

1. high-point-checker - 爽点密度检查
2. consistency-checker - 设定一致性检查
3. pacing-checker - 节奏检查
4. ooc-checker - 人物 OOC 检查
5. continuity-checker - 连贯性检查

## 使用示例

```
/webnovel-review 1-10       # 审查第 1-10 章
/webnovel-review 41-50      # 审查第 41-50 章
```

## 输出

生成 `审查报告/第XXX-XXX章审查报告.md`，包含：
- 5 个维度的评分
- 具体问题和修改建议
- 整体质量评价
