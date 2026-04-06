```sql
select * from vela_test_verification_session order by created desc;

select * from vela_test_workflow where session_id = 'vs-20260406-9a086c';

select * from vela_test_build_record where workflow_id = 'cw-20260406-9f5aef';

SELECT * FROM case_test_task WHERE workflow_id = 'cw-20260406-9f5aef';

select * from case_test_task_histories where task_id = 1345;
```