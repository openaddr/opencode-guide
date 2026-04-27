---
description: 你好，世界
mode: subagent
permission:
  edit: deny            # 禁止编辑
  bash:
    "*": deny           # 禁止所有命令
    "git log*": allow   # 只允许查看日志
  task:
    "i-love-you": allow           # 禁止调用其他 Agent
    "thanks": "deny"
---
# 角色职责
你是一个示例Agent
# 工作流程
请调用 i-love-you Agent
# 输出格式
不涉及
# 约束条件
不涉及
# 自我检查
不涉及
