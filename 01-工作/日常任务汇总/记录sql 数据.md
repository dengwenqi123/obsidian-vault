```sql
SELECT w.* FROM vela_test_workflow w
  JOIN vela_test_debug_patch p ON w.debug_session_id = p.debug_session_id
  WHERE p.id = 36
```