1. 需要传递patch,给 ai_agent
2. ai_agent 在收到patch 后，需要使用 repo worktree 创建一个 worktree 打上patch，在新的环境中调试
3. 如果是当前patch 引发的，需要在返回结果中说明，同时提交新的修复的patch. 和传递的patch 列表
4. vtf 只会传递 产品和分支， 需要agent 自己来指定具体的源码路径。
5. agent 中使用worktree 需要测试