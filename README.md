# pgAdmin
# Tutorial of pgAdmin
<details open="open">
  <summary><b>Table of Contents</b></summary>
  <ol>
    <li>
      <a href="#introduction">Introduction</a>
    </li>
    <li>
      <a href="#tables">Tables</a>
      <ul>
        <li><a href="#etl-tables">etl tables</a></li>
	<li><a href="#set-tables">set tables</a></li>
      </ul>
    </li>
    <li>
      <a href="#the-syntax">The Syntax</a>
      <ul>
        <li><a href="#etl_tables">etl_tables</a></li>
	<ul>
	<li><a href="#etl_flow">etl_flow</a></li>
	<li><a href="#etl_qtime_spec">etl_qtime_spec</a></li>
	<li><a href="#etl_wip">etl_wip</a></li>
        <li><a href="#etl_rls">etl_rls</a></li>
        <li><a href="#etl_tool">etl_tool</a></li>
	<li><a href="#etl_mask_info">etl_mask_info</a></li> 
	<li><a href="#etl_demand">etl_demand</a></li>
	<li><a href="#etl_lothistory">etl_lothistory</a></li>
        <li><a href="#etl_stage_move">etl_stage_move</a></li>
        <li><a href="#etl_backup_hist">etl_backup_hist</a></li>
	<li><a href="#etl_photo_balance">etl_photo_balance</a></li>
	<li><a href="#etl_safety_wip">etl_safety_wip</a></li>
	<li><a href="#etl_pri_wip">etl_pri_wip</a></li>
	<li><a href="#etl_pirun">etl_pirun</a></li>
	<li><a href="#etl_backup_rls">etl_backup_rls</a></li>
	<li><a href="#etl_backup_report">etl_backup_report</a></li>
	<li><a href="#etl_kpi_daily">etl_kpi_daily</a></li>  
	<li><a href="#etl_kpi_hourly">etl_kpi_hourly</a></li>
	</ul> 
	<li><a href="#set_tables">set_tables</a></li>
	<ul>
	<li><a href="#set_ver_control">set_ver_control</a></li>
	<li><a href="#set_small_lot">set_small_lot</a></li>
	<li><a href="#set_lot_hold">set_lot_hold</a></li>
        <li><a href="#set_monitor">set_monitor</a></li>
        <li><a href="#set_recipe_group">set_recipe_group</a></li>
	<li><a href="#set_setup">set_setup</a></li>
	<li><a href="#set_backup_report">set_backup_report</a></li>
	<li><a href="#set_system">set_system</a></li>
	<li><a href="#set_wip_weighting">set_wip_weighting</a></li>
	<li><a href="#set_tool_down">set_tool_down</a></li>
	</ul> 
      </ul>
    </li>
    <li>
      <a href="#Another-way-to-check-the-latest-version">Another way to check the latest version</a>
    </li>
    <li>
      <a href="#Data-verification">Data verification</a>
      <ul>
        <li><a href="#etl-flow">etl flow</a></li>
      </ul>
    </li>      
  </ol>
</details>

# __Introduction__
This repository is a tutorial for __pgAdmin 4__, including the script for searching some specific data.
# __Tables__
## __etl tables__
* **etl_flow**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| prod_id  | Product ID  |
| plan_id  | Process/Plan/Route ID |
| step_id | 站點編號 |
| layer | 製程層名稱 |
| stage | 站點Stage |
| toolg_id | 機群名稱 |
| recipe | 站點Recipe |
| reticle_group | 光罩群組 |
| step_type | 站點類別(N為一般站點；R為重工站點) |
| toolg_type | 機群加工類別(P為一般製程機群；M為量測機群) |
| process_time | 製程處理時間 = Track Out Time – Track In Time (單位：小時) |
| cycle_time | 站點週期時間 = Track Out Time – Arrival Time (單位：小時) |
| update_time | 資料更新時間 |
| plan_no | Process/Plan/Route 順序 |

* **etl_qtime_spec**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| prod_id  | Product ID  |
| plan_id  | Process/Plan/Route ID |
| step_id_from | Qtime限制起點站點編號 |
| step_id_to | Qtime限制終點站點編號 |
| timelimit | Qtime限制長度 |
| update_time | 資料更新時間 |

* **etl_wip**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| lot_id | Lot名稱 |
| step_id  | 站點編號 |
| target_step_id  | 目標站點編號  |
| target_toolg_id | 目標機群 |
| prod_id  | Product ID |
| plan_id | Process/Plan/Route ID |
| lot_type | Lot類型 |
| qty | 片數 |
| pty | Lot的優先順序 |
| shr_flag | Super Hot Lot分類(支援0~4，-1為Normal Lot) |
| lot_status | Lot狀態(僅排running, wait, jobprepared) |
| remain_qtime | 還有多久會發生Over Qtime (最嚴苛)，若無Qtime限制，設為999，負數視為已over (單位：小時) |
| qtime_step_id_to | Qtime終點站點編號 |
| arrival | 到站時間 |
| tool_id | 機台名稱 |
| reticle_id | 光罩名稱 |
| recipe | 站點Recipe |
| ppid | 機台Recipe (可能含Chamber/參數資訊) |
| track_in | move in 進機時間 |
| process_start | 製程起始時間 (抽片Run) |
| tech_id | Technology Name |
| customer | Customer ID |
| location | Lot所在位置 (樓層/走道) |
| assign_tool_id | 指定機台名稱 |
| update_time | 資料更新時間 |
| stage | 站點Stage |
| target_plan_id | 目標站點Process/Plan/Route ID |
| rack | (客製化) Lot所在貨架名稱 |

* **etl_rls**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| lot_id  | Lot 名稱 |
| target_step_id  | 目標站點編號  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| recipe  | 站點Recipe  |
| ppid | 機台Recipe (可能含Chamber/參數資訊)  |
| reticle_id  | 光罩名稱 |
| ch_set  | Chamber 組合名稱 |
| set_status  | 機限狀態，"ACTIVE"視為可用，其餘視為機限禁用 |
| non_process_time  | 非製程處理時間 (單位：小時) |
| process_time  | 機台製程處理時間 (單位：小時) |
| update_time  | 資料更新時間 |
| target_stage  | 目標站點Stage |
| remark  | (客製化) 備註 |

* **etl_tool**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| tool_status  | 主機台機況 (僅排 RUN, IDLE) |
| tool_status_time  | 機台切機況時間 |
| ch_status  | Chamber 機況 (僅排 RUN, IDLE) |
| ch_status_time  | Chamber 切機況時間 |
| lot_id  | 最後一批Track In Lot ID |
| down_back_time  | 機況預估回線時間 |
| port_num  | 機台 Load port 數量 |
| reticle_num  | 光罩儲位數量 |
| location  | 機台位置 (樓層/走道) |
| update_time  | 資料更新時間 |

* **etl_mask_info**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| reticle_group  | 光罩群組 |
| reticle_id  | 光罩名稱 |
| reticle_count  | 光罩可用數量 |
| position  | 光罩位置 (若在傳送中，則為預訂到達目的地機台) |
| position_time  | 光罩抵達時間 |
| reticle_status  | 光罩狀態 (僅排ACTIVE) |
| inspection_time  | 下次排檢時間 |
| run_qty  | 已使用 wafer 數量 |
| run_lbound  | 使用 wafer 片數排檢下限 |
| run_ubound  | 使用 wafer 片數排檢上限 |
| update_time  | 資料更新時間 |

* **etl_demand**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| prod_id  | Product ID |
| plan_id | Process/Plan/Route ID |
| step_id  | 站點編號 |
| lot_type  | Lot 類型 |
| tech_id  | Technology Name |
| customer | Customer ID |
| recipe  | 站點Recipe |
| layer_group  | Layer 群組 |
| layer | 製程層名稱 |
| stage | 站點Stage |
| lot_id | Lot 名稱 |
| pty | Lot 的優先順序 |
| target_qty | 目標量 |
| target_shift | 班次 |
| target_time_from | 起算時間 |
| target_time | 結算時間 |
| target_mode | 目標模式 (0 = 至少；1 = 至多，預設為0) |
| update_time  | 資料更新時間 |
| mfg_date  | 生產日期 |
| mtd_qty  | (客製化) MTD目標量 |
| dynamic_qty  | (客製化) 動態目標量 |
| prod_name  | (客製化) 特殊製程名稱 |
| tool_id  | 機台名稱 |
| move_mode | (客製化) 扣除已過量模式 |
| seq | 規則優先順序 (小-->大) |

* **etl_lothistory**

| Column  | Description |
| ------------- | ------------- |
| lot_id  | Lot 名稱 |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| prod_id  | Product ID |
| plan_id | Process/Plan/Route ID |
| step_id  | 站點編號 |
| lot_type  | Lot 類型 |
| pty | Lot 的優先順序 |
| shr_flag  | Super Hot Lot 分類 (支援 0~4，-1為 Normal Lot) |
| layer | 製程層名稱 |
| stage | 站點Stage |
| recipe  | 站點Recipe  |
| ppid  | 機台Recipe (可能含Chamber/參數資訊) |
| reticle_id  | 光罩名稱 |
| qty | 片數 |
| tech_id  | Technology Name |
| customer | Customer ID |
| arrival | 到站時間 |
| job_prepare | 準備派送時間 (已鎖定機台) |
| track_in | move in 進機時間 |
| process_start | 製程起始時間 (抽片Run) |
| process_end | 製程結束時間 |
| track_out | move out 出機時間 |
| rework_flag | 是否重工 (Y = 重工，N = 非重工) |
| backup_flag | 是否代工 (B = 他廠代工，BF = 代工他廠；N = 非代工) |
| update_time  | 資料更新時間 |
| waferchamberinfo  | (客製化) 測機項目資訊 |
| flagfield  | ETL 程式比對來源表與目標表的差異 |

* **etl_stage_move**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| mfg_date  | 生產日期 |
| toolg_id  | 機群名稱 |
| tech_id  | Technology Name |
| stage | 站點Stage |
| lot_type  | Lot 類型 |
| qty | 片數 |
| update_time  | 資料更新時間 |
| prod_id  | Product ID |
| customer | Customer ID |
| measure_qty | 量測站堆貨數量 |

* **etl_backup_hist**

| Column  | Description |
| ------------- | ------------- |
| mfg_date  | 生產日期 |
| seq_id  | 小時數 |
| toolg_id  | 機群名稱 |
| tech_id  | Technology Name |
| layer_group  | Layer 群組 |
| qty | 片數 |
| update_time  | 資料更新時間 |
| flagfield  | ETL 程式比對來源表與目標表的差異 |

* **etl_photo_balance**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| assign_tool_id  | 指定機台名稱 |
| qty | 片數 |
| update_time  | 資料更新時間 |

* **etl_safety_wip**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| safety_wip_lb  | 安全存量下限 |
| safety_wip_ub  | 安全存量上限 |
| onhand_qty  | 當站wip片數 |
| coming_qty   | 未到站 (黃光-蝕刻站間) WIP 片數 |
| update_time  | 資料更新時間 |
| subgroup  | 子群組 |
| prod_mode  | Product 比對模式 |
| prod_id | Product ID |
| tech_mode  | Tech 比對模式 |
| tech_id  | Technology Name |
| recipe_mode  | Step Recipe 比對模式 |
| recipe  | 站點 Recipe |

* **etl_pri_wip**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| lot_id  | Lot 名稱 |
| stage | 站點Stage |
| update_time  | 資料更新時間 |
| pri_type  | 優先類型 |

* **etl_pirun**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| prod_id | Product ID |
| plan_id | Process/Plan/Route ID |
| step_id  | 站點編號 |
| recipe  | 站點 Recipe |
| ppid  | 機台Recipe (可能含Chamber/參數資訊) |
| stage | 站點Stage |
| tech_id  | Technology Name |
| customer | Customer ID |
| lot_id  | Lot 名稱 |
| rule_name  | 規則名稱 |
| remaining_count  | 剩餘批數 (超過後會禁Run) |
| remaining_time  | 剩餘時數 (超過後會禁Run) |
| recover_time  | 回線時間 (如：Monitor 加測時間) |
| valid_recipe  | 可延長時效的 Recipe |
| valid_time  | 可延長的時間 |
| update_time  | 資料更新時間 |

* **etl_backup_rls**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| tool_model  | 外廠機台機型  |
| reticle_id  | 光罩名稱 |
| prod_id_6  | Product ID 前6碼  |
| stage | 站點Stage |
| onhand_qty  | 當站 WIP 數量 |
| coming_qty  | 當日 flow in WIP 數量 |
| update_time  | 資料更新時間 |

* **etl_backup_report**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| factory_id  | 工廠名稱 |
| commit_qty  | 廠別可支援量 |
| toolg_id  | 外廠機群名稱 |
| tool_model  | 外廠機台機型 |
| initial_qty  | 期初外廠黃光機台 WIP 量 |
| today_qty  | 當日量 |
| safety_qty  | 安全水位數量 |
| update_time  | 資料更新時間 |

* **etl_kpi_daily**

| Column  | Description |
| ------------- | ------------- |
| mfg_date  | 生產日期 |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| kpi | KPI 名稱 (縮寫) |
| value  | KPI 數值 |
| update_time  | 資料更新時間 |
| flagfield  | ETL 程式比對來源表與目標表的差異 |

## __set tables__
* **set_ver_control**

| Column  | Description |
| ------------- | ------------- |
| id  | Version number (版本號)  |
| module_id  | 區域名稱 |
| toolg_id  | 機群名稱 |
| table_name  | Table 名稱 |
| name  | 更新者 |
| version  | 版本數 |
| activeflag  | 生效開關 (預設 1) |
| enableflag  | 開關 |
| description  | 敘述 |
| update_time  | 資料更新時間 |
| update_user  | 資料更新者 |

* **set_small_lot**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| neighbor_lot  | 連續批數 |
| demand_qty  | 連續最小片數 |

* **set_lot_hold**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| lot_id  | Lot 名稱 |
| pty | Lot 的優先順序 |
| prod_id | Product ID |
| plan_id | Process/Plan/Route ID |
| step_id  | 站點編號 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| start_time  | 開始時間 |
| end_time | 結束時間 |
| action  | Lot Hold 類型 (禁用/ Assign) |
| repeat_daily | 是否每日重複 |
| lot_type  | Lot 類型 |
| recipe  | 站點 Recipe |
| ppid  | 機台 Recipe |
| layer  | 製程層名稱 |
| stage | 站點 Stage |
| tech_id  | Technology Name |

* **set_monitor**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| job_id  | Monitor Job 名稱 |
| start_date  | Monitor 建立時間 |
| end_date  | Monitor 截止時間 |
| process_time  | Monitor Process Time |
| reticle_id  | 光罩名稱 |
| weekday  | Monitor 每週測機日 (1~7) |
| update_time  | 資料更新時間 |
| target_shift  | 班次 |
| weekly_flag  | 週重複開關 |

* **set_recipe_group**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| recipe  | 站點 Recipe |
| recipe_group  | Recipe 群組名稱 |

* **set_setup**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號)  |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| seq  | 規則優先序 (小-->大) |
| process_time | Setup 處理時間 (單位：小時) |
| prod_last | 前批 Lot 的 Product ID |
| prod_next | 當前 Lot 的 Product ID |
| plan_last | 前批 Lot 的 Route ID |
| plan_next | 當前 Lot 的 Route ID |
| layer_last | 前批 Lot 的 Layer |
| layer_next | 當前 Lot 的 Layer |
| stage_last | 前批 Lot 的 Stage |
| stage_next | 當前 Lot 的 Stage |
| recipe_last | 前批 Lot 的 Recipe |
| recipe_next | 當前 Lot 的 Recipe |
| recipe_group_last | 前批 Lot 的 Recipe Group |
| recipe_group_next | 當前 Lot 的 Recipe Group |
| recipe_setup_last | 前批 Lot 的 Recipe Setup |
| recipe_setup_next | 當前 Lot 的 Recipe Setup |
| ppid_last | 前批 Lot 的 EQP Recipe |
| ppid_next | 當前 Lot 的 EQP Recipe |
| process_cost | Setup 權重 |


* **set_backup_report**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號) |
| factory_id  | 工廠名稱|
| commit_qty | 廠別可支援量 |
| toolg_id  | 機群名稱 |
| tool_model  | 外廠機台機型 |
| tool_id  | 外廠機台名稱 |
| safety_lb_coe  | 安全水位下限倍率 |
| safety_ub_coe  | 安全水位上限倍率 |
| update_time  | 資料更新時間 |

* **set_system**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號) |
| id  | ID |
| propertyno  | 排程參數名稱 |
| propertyvalue  | 參數數值 |
| remark  | 備註 |

* **set_wip_weighting**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號) |
| toolg_id  | 機群名稱 |
| lot_id  | Lot 名稱 |
| pty | Lot 的優先順序 |
| prod_id | Product ID |
| step_id  | 站點編號 |
| weighting  | 權重值 |
| effective_time  | 生效時間 |
| lot_type  | Lot 類型 |
| long_stay  | Lot 到站多久之後考量權重 |
| recipe  | 站點 Recipe |
| stage  | 站點 Stage |
| wait  | Lot 到站多久以內考量權重 |
| tech_id  | Technology Name |

* **set_tool_down**

| Column  | Description |
| ------------- | ------------- |
| parentid  | Version number (版本號) |
| toolg_id  | 機群名稱 |
| tool_id  | 機台名稱 |
| ch_id  | Chamber 名稱 |
| down_start  | 當機起始時間 |
| down_end  | 當機結束時間 |
| remark  | 備註 |


# __The Syntax__
## __etl_tables__
### __etl_flow__
**1. Select the newest version of etl_flow and extract 100 data**
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_flow' **order by** update_time **desc** **limit** 100;  

**2. Find the specific parentid and order the data by prod_id, plan_no, step_id**
* **select** * **from** yth.etl_flow **where** parentid = 'e69121eb-55af-04b5-e053-24017e0a9724' **order by** prod_id, plan_no, step_id;
    
**3. Just give the number to the data, if the prod_id is the same, then it will give the number in ascending order**

(1)  
* **select**   
	**row_number()** **over** (**partition by** prod_id **order by** plan_no, step_id) **as** rtn, *  
**from** yth.etl_flow;  
**where** parentid = 'e17f9d53-1e23-141f-e053-24017e0a7d15'  
**order by** prod_id, plan_no, step_id  
**limit** 1000;  

(2)  
* **select** * **from** yth.etl_flow **limit** 100;
* **select**  
	**row_number()** **over**(**partition by** prod_id **order by** plan_no, step_id) **as** rtn, *  
**from** yth.etl_flow  
**where** parentid = 'c7d78df4-91d6-517f-e053-24017e0a85af' **and** prod_id='VP4611F-TBR1HAZ1.02'  
**order by** prod_id, plan_no, step_id;

Note: Different prod_id has differnt groups of numbers

### __etl_qtime_spec__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_qtime_spec' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_qtime_spec **where** parentid = 'e1814a4d-2431-0ece-e053-24017e0af009' **order by** prod_id, step_id_from;

**Checking how many steps it goes through** 
* **select** * **from** yth.etl_flow  
**where** parentid = 'e1814a4d-2431-0ece-e053-24017e0af009'  
**and** prod_id = 'BK-V2-DPVT-2-3.02'  
**and** plan_id = 'BK-V2-DPVT-2-3.02'  
**and** step_id >= '008.000'  
**and** step_id <= '011.000'  
**order by** prod_id, plan_no, step_id;

### __etl_wip__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_wip' **order by** update_time **desc** **limit** 100;

**1. Determine whether it is a current stage**  
* **select** * **from** yth.etl_wip  
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'     
**and** step_id = target_step_id **and** plan_id = target_plan_id --onhand lot  
**limit** 100; 

**2. Checking how many onhand lot that ILINE has**
* **select** * **from** yth.etl_wip  
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'     
**and** target_toolg_id = 'ILINE'  
**and** step_id = target_step_id **and** plan_id = target_plan_id --onhand lot;  

**3. Checking how many steps will go through**
* **select** * **from** yth.etl_wip    
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'  
**and** target_toolg_id = 'ILINE'  
**and** **not** (step_id = target_step_id **and** plan_id = target_plan_id) --onhand lot;  

**4. Using "like" to find the specific word in column plan_id**
* **select** * **from** yth.etl_wip   
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'    
**and** target_toolg_id = 'ILINE'   
**and** step_id = target_step_id **and** plan_id = target_plan_id --onhand lot    
**and** plan_id **like** '%RWK%';  

### __etl_rls__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_rls' **order by** update_time **desc** **limit** 100;
* **select** * **from** yth.etl_rls  
**where** parentid = 'e18828bf-31d6-16ee-e053-24017e0aa58d'   
**order by** lot_id, target_step_id, tool_id **limit** 1000;

### __etl_tool__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_tool' **order by** update_time **desc** **limit** 100;
* **select** * **from** yth.etl_tool    
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc';
* **select** * **from** yth.etl_tool      
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'ILINE';
* **select** * **from** yth.etl_tool    
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'SPUTTER';
* **select** * **from** yth.etl_tool   
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'SPUTTER'  
**order by** tool_id, ch_id;

### __etl_mask_info__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_mask_info' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_mask_info  
**where** parentid = 'e188f944-d0a6-41ca-e053-24017e0a9c9f';  

**Find the machine in the position column**     
* **select** * **from** yth.etl_mask_info   
**where** parentid = 'e188f944-d0a6-41ca-e053-24017e0a9c9f'  
**and** **position in** (**select** tool_id **from** yth.etl_tool **where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc');

### __etl_demand__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_demand' **order by** update_time **desc** **limit** 100;

**Key stage demand** 
* **select** * **from** yth.etl_demand   
**where** parentid = 'e188d57c-4426-4cf2-e053-24017e0adc95'  
**and** seq = 1;

### __etl_lothistory__
* **select** * **from** yth.etl_demand **where** parentid = 'e188d57c-4426-4cf2-e053-24017e0adc95'  
**and** seq = 3;
* **select** * **from** yth.etl_lothistory   
**where** track_out >= '2022-06-16 07:20'  
**order by** tool_id, track_in;  
* **select** * **from** yth.etl_lothistory     
**where** track_out >= '2022-06-16 07:20'    
**and** toolg_id = 'ILINE'  
**order by** tool_id, track_in;
* **select** * **from** yth.etl_lothistory   
**where** track_out >= '2022-06-16 07:20'    
**and** toolg_id = 'ILINE'    
**and** stage **in** ('ALZER-Z', 'ALZER', 'ALZER-1')  
**order by** tool_id, track_in;

### __etl_stage_move__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_stage_move' **order by** update_time **desc** **limit** 100;  

* **select** * **from** yth.etl_demand    
**where** parentid = 'e188d57c-4426-4cf2-e053-24017e0adc95'      
**and** seq = 1;

**Pick one specific stage from etl_demand and search in the etl_stage_move** 
* **select** * **from** yth.etl_stage_move
**where** parentid = 'e1894723-d41b-3f0d-e053-24017e0a206c'  
**and** stage = 'ALHNSD';

### __etl_backup_hist__
* **select** * **from** yth.etl_backup_hist **order by** update_time;
* **select** * **from** yth.etl_backup_hist **order by** update_time **desc**;

### __etl_photo_balance__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_photo_balance' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_photo_balance **where** parentid = 'e19bb18a-cb46-176a-e053-24017e0a79f7';

### __etl_safety_wip__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_safety_wip' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_safety_wip **where** parentid = 'e19c05f8-2fed-3ad4-e053-24017e0a5d21';

### __etl_pri_wip__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_pri_wip' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_pri_wip **where** parentid = 'e19bdb02-e8cc-2e72-e053-24017e0a43e8';

**Check how many pri_types**
* **select** **distinct** pri_type **from** yth.etl_pri_wip **where** parentid = 'e19bdb02-e8cc-2e72-e053-24017e0a43e8';

### __etl_pirun__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_pirun' **order by** update_time **desc** **limit** 100;   
* **select** rule_name, * **from** yth.etl_pirun **where** parentid = 'e19c30eb-5224-4813-e053-24017e0a9c28'  
**order by** toolg_id, tool_id, rule_name;  
* **select** update_time, rule_name, remaining_time, * **from** yth.etl_pirun **where** prod_id = 'VP5123J-C2T2NAZ1.01'  
**and** plan_id = '25UBCA-V1-N.13'   
**and** step_id = '432.000'  
**and** tool_id = '1B-D300'  
**and** rule_name = 'SOC'    
**order by** update_time **desc limit** 100;

### __etl_backup_rls__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_backup_rls' **order by** update_time **desc** **limit** 100; 
* **select** * **from** yth.etl_backup_rls **where** parentid = 'e19449f8-7d3c-55a6-e053-24017e0a75f4';

### __etl_backup_report__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_backup_report' **order by** update_time **desc** **limit** 100; 
* **select** * **from** yth.etl_backup_report **where** parentid = 'e1997525-f46d-4994-e053-24017e0a1ddb';

### __etl_kpi_daily__
* **select** * **from** yth.etl_kpi_daily **order by** update_time **desc** **limit** 100;

### __etl_kpi_hourly__
* **select** * **from** yth.etl_kpi_hourly **order by** update_time **desc** **limit** 100;

## __set_tables__
### __set_ver_control__
* **select** * **from** yth.v_set_ver_control;

### __set_small_lot__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_small_lot' **order by** update_time **desc**;     
* **select** * **from** yth.set_small_lot **where** parentid = '4da07a39-84e1-4f99-8834-139d82d872af';   

### __set_lot_hold__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_lot_hold' **order by** update_time **desc**;     
* **select** * **from** yth.set_lot_hold **where** parentid = 'a7e3f17a-f033-11ec-81a1-6fbc590a0e3f';  

### __set_monitor__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_monitor' **order by** update_time **desc**;         
* **select** * **from** yth.set_monitor **where** parentid = 'e816c920-062d-11ec-a078-d7f01e67cd54';      

### __set_recipe_group__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_recipe_group' **order by** update_time **desc**;  
* **select** * **from** yth.set_recipe_group **where** parentid = '68107ecc-da7d-11ec-8f5f-0bb88faf0213';        

### __set_setup__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_setup' **order by** update_time **desc**;  
* **select** * **from** yth.set_setup **where** parentid = '82e2f365-d0a1-481c-a396-c843c43ed36b';     
* **select** * **from** yth.set_setup **where** parentid = '82e2f365-d0a1-481c-a396-c843c43ed36b'
**and** stage_next = ' '  
**and** ppid_next = ' '    
**order by** recipe_setup_next, recipe_setup_last;    
* **select** * **from** yth.set_setup **where** parentid = '82e2f365-d0a1-481c-a396-c843c43ed36b'  
**and** stage_next = ' '  
**and** ppid_next = ' '  
**order by** process_time;    
* **select** process_time, process_cost, * **from** yth.set_setup     
**where** parentid = '82e2f365-d0a1-481c-a396-c843c43ed36b'  
**and** stage_next = ' '    
**and** ppid_next = ' '    
**order by** process_time;  

### __set_backup_report__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_backup_report' **order by** update_time **desc**;   
* **select** * **from** yth.set_backup_report **where** parentid = 'a47e5844-d00e-11ec-93c9-3bf99e383281';  

### __set_system__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_system' **order by** update_time **desc**;     
* **select** * **from** yth.set_system **where** parentid = '3296900a-f031-11ec-8278-33ffb447eb5d';    

### __set_wip_weighting__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_wip_weighting' **order by** update_time **desc**;  
* **select** * **from** yth.set_wip_weighting **where** parentid = '84877e12-eb5c-11ec-81c7-4f7f7143ff37' **order by** pty;   

### __set_tool_down__
* **select** * **from** yth.set_ver_control **where** **table_name** = 'set_tool_down' **order by** update_time **desc**;    
* **select** * **from** yth.set_tool_down **where** parentid = '31c1cf3e-4e68-11ec-ace7-6f0fb693468e';      


# __Another way to check the latest version__
Except using **etl_ver_control** to check the latest version, you can use **v_** to check  
* **v_etl_photo_balance**      
  **select** * **from** yth.v_etl_photo_balance  
* **v_etl_flow**    
  **select** * **from** yth.v_etl_flow **order by** prod_id, plan_no, step_id **limit** 1000;  
* **v_etl_wip**      
  (1) **select** **distinct** lot_type **from** yth.v_etl_wip **where** target_toolg_id = 'ILINE';    
  (2) **select** **distinct** lot_type **from** yth.v_etl_wip **where** target_toolg_id = 'DUV';     


# __Data verification__
## __etl flow__
**1. Specific products and stops in the itinerary are not repeated** 
* **select** * **from** yth.v_etl_flow **order by** prod_id, plan_no, step_id **limit** 1000;  
with t1 **as** (**select** **row_number()** **over** (**partition by** prod_id, plan_id, plan_no, step_id **order by** cycle_time) **as** rtn * **from** yth.v_etl_flow) **select** **count** (*) **from** t1 **where** rt > 1





