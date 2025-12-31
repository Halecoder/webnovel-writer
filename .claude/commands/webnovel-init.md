---
allowed-tools: Bash, Write, Read, AskUserQuestion
argument-hint: [题材类型] | 留空交互式选择
description: 初始化网文项目，生成设定集和大纲框架。创建 AI 工作室的完整项目结构。
---

# /webnovel-init

初始化网文创作项目，创建"AI 工作室"所需的完整文件结构。

## 执行流程

### Step 1: 检测现有项目
```bash
if [ -f ".webnovel/state.json" ]; then
    询问用户是否覆盖现有项目
fi
```

### Step 2: 选择题材

使用 AskUserQuestion 让用户选择题材类型：

```json
{
  "questions": [{
    "header": "题材选择",
    "question": "请选择您的小说题材类型？",
    "options": [
      {"label": "修仙（系统流）", "description": "经典修仙 + 金手指系统，适合新手"},
      {"label": "都市异能", "description": "现代背景 + 超能力"},
      {"label": "玄幻穿越", "description": "异世界 + 穿越重生"},
      {"label": "游戏网游", "description": "虚拟现实/网游世界"},
      {"label": "科幻星际", "description": "未来科技/星际争霸"}
    ],
    "multiSelect": false
  }]
}
```

### Step 3: 基础信息收集

继续询问：
- 小说标题
- 主角姓名
- 一句话简介（可选）

### Step 4: 调用 Python 脚本初始化

```bash
python .claude/skills/webnovel-writer/scripts/init_project.py "./webnovel-project" "小说标题" "题材类型"
```

这将创建：
```
webnovel-project/
├── .webnovel/
│   ├── state.json          # 项目状态
│   └── backups/
├── 设定集/
│   ├── 世界观.md           # 根据题材模板生成
│   ├── 力量体系.md
│   ├── 主角卡.md
│   └── 角色库/
├── 大纲/
│   └── 总纲.md             # 卷-篇-章结构
├── 正文/
└── 审查报告/
```

### Step 5: 调用 webnovel-writer skill 生成初始设定

```
Skill: webnovel-writer
Mode: Plan
Task: 根据题材模板生成世界观、主角卡和总纲
```

### Step 6: 输出提示

```
✅ 项目初始化完成！

📁 项目路径: ./webnovel-project
📚 题材: 修仙（系统流）
👤 主角: 林天

✨ 已生成文件:
- 设定集/世界观.md
- 设定集/主角卡.md
- 大纲/总纲.md（8 卷框架）

🎯 下一步操作:
1. 查看并调整设定集（可手动编辑）
2. 运行 /webnovel-plan 1 规划第 1 卷详细大纲
3. 运行 /webnovel-write 1 开始创作第 1 章
```

## 注意事项

- 初始化后会自动打开项目目录
- 所有文件均为 Markdown 格式，可手动编辑
- state.json 由系统自动维护，建议不要手动修改
