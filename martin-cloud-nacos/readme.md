删除 5天前的binlog

show binary logs;
PURGE MASTER LOGS BEFORE DATE_SUB(CURRENT_DATE, INTERVAL 5 DAY); 