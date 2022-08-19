# pgAdmin
This is for recording the script of the database

Select the newest version of etl_flow
1. select * from yth.etl_ver_control where table_name = 'etl_flow' order by update_time desc limit 100;

2.select * from yth.etl_flow
  where parentid = 'e69121eb-55af-04b5-e053-24017e0a9724'
  order by prod_id, plan_no, step_id;
