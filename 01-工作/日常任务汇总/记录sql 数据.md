```sql
SELECT w.* FROM vela_test_workflow w
  JOIN vela_test_debug_patch p ON w.debug_session_id = p.debug_session_id
  WHERE p.id = 36
```


1. 需要跑通耳机项目的自动化分析流程
2. 需要区分本地环境和线上环境
3.  列出最近解bug 所有的任务清单


4. 提交patch  ai agent 需要在节点上验证是否提交的 patch 准确
5. 