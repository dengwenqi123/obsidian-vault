```sql
select * from vela_test_workflow where workflow_id = 'cw-20260411-ff4062';
select * from vela_test_workflow where session_log_url is not null;



select * from vela_test_workflow where session_id = 'vs-20260411-5183ea';

select * from vela_test_build_record where workflow_id = 'cw-20260411-ff4062';

select task_status from case_test_task where workflow_id = 'cw-20260411-ff4062';

select * from case_test_task_histories where task_id = 1426;

select * from case_test_task;
  SELECT vtw.workflow_id, ctt.task_status, ctth.coral_run_task_id
        FROM vela_test_workflow vtw
        INNER JOIN case_test_task ctt ON vtw.workflow_id = ctt.workflow_id
        INNER JOIN case_test_task_histories ctth ON ctt.task_id = ctth.task_id
        WHERE ctt.workflow_id IS NOT NULL
          AND ctt.task_status IN ('finished', 'trigger_test_failed', 'env_failed')
          AND vtw.state = 'VERIFYING';
          
          update vela_test_verify_record set task_id = '1795311' where id = 6;
          
select * from vela_test_verify_record where workflow_id = 'cw-20260411-ff4062';

select * from vela_test_verification_session where session_id  = 'vs-20260411-907d33';
```

# 更新点
1. 默认模型都更新为 4.7 暂时不升级到 4.7
2.  需要重新安装python 的依赖库

pip install 'starlette>=0.37.2,<0.39.0' 

git config --global --add safe.directory /tools/ai-agent-service/prompts

1. 请问现在 AI 分析，pa

仓库获取错误


1. 更新matrix 节点， 增加 lief-0.17.0 库
2. pip install -U lief-0.17.0.dev0-cp310-cp310-linux_x86_64.whl

优先看是不是项目代码是否有问题，如果被测代码没有问题，在开始检查是否是测试用例的问题。

获取修改用户的方式，调整为： 最近修改该文件的owner

优先排查**项目代码**是否存在问题；若确认被测代码无异常，再逐一核查**测试用例**本身的问题。
之前获取到的是仓库路径，不是具体的Gerrit仓库名称. 同时，获取Gerrit 仓库名称，一定要进入到修改文件的目录，再获取，因为存在仓库嵌套

提单：
1. crash 按照程序名
2. 异常场景， 按照不同的类型的remark 配置
3. 