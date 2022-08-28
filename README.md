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
    </li>
    <li>
      <a href="#the-script">The script</a> 
      <ul>
        <li><a href="#etl_flow">etl_flow</a></li>
	<li><a href="#etl_qtime_spec">etl_qtime_spec</a></li>
        <li><a href="#etl_wip">etl_wip</a></li>
	<li><a href="#etl_rls">etl_rls</a></li>
	<li><a href="#etl_tool">etl_tool</a></li>
	<li><a href="#etl_mask_info">etl_mask_info</a></li> 
	<li><a href="#etl_demand">etl_demand</a></li>
	<li><a href="#etl_lothistory">etl_lothistory</a></li>
      </ul>
    </li>
    <li>
      <a href="#the-instructions-for-this-database">The instructions for this database</a>
    </li>
    
  </ol>
</details>

# __Introduction__
This repository is a tutorial for __pgAdmin 4__, including the script for searching some specific data.
# __Tables__
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

# __The script__
## __etl_flow__
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
	**row_number()** **over**(**partition by** prod_id **order by** plan_no, step_id)**as** rtn, *  
**from** yth.etl_flow  
**where** parentid = 'c7d78df4-91d6-517f-e053-24017e0a85af' **and** prod_id='VP4611F-TBR1HAZ1.02'  
**order by** prod_id, plan_no, step_id

Note: Different prod_id has differnt groups of numbers

## __etl_qtime_spec__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_qtime_spec' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_qtime_spec **where** parentid = 'e1814a4d-2431-0ece-e053-24017e0af009' **order by** prod_id, step_id_from

**1. Checking how many steps it goes through** 
* **select** * **from** yth.etl_flow  
**where** parentid = 'e1814a4d-2431-0ece-e053-24017e0af009'  
**and** prod_id = 'BK-V2-DPVT-2-3.02'  
**and** plan_id = 'BK-V2-DPVT-2-3.02'  
**and** step_id >= '008.000'  
**and** step_id <= '011.000'  
**order by** prod_id, plan_no, step_id;

## __etl_wip__
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
**and** step_id = target_step_id **and** plan_id = target_plan_id --onhand lot  

**3. Checking how many steps will go through**
* **select** * **from** yth.etl_wip    
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'  
**and** target_toolg_id = 'ILINE'  
**and** **not** (step_id = target_step_id **and** plan_id = target_plan_id) --onhand lot  

**4. Using "like" to find the specific word in column plan_id**
* **select** * **from** yth.etl_wip   
**where** parentid = 'e6d1247c-741d-74e6-e053-24017e0a2201'    
**and** target_toolg_id = 'ILINE'   
**and** step_id = target_step_id **and** plan_id = target_plan_id --onhand lot    
**and** plan_id **like** '%RWK%'  

## __etl_rls__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_rls' **order by** update_time **desc** **limit** 100;
* **select** * **from** yth.etl_rls  
**where** parentid = 'e18828bf-31d6-16ee-e053-24017e0aa58d'   
**order by** lot_id, target_step_id, tool_id **limit** 1000;

## __etl_tool__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_tool' **order by** update_time **desc** **limit** 100;
* **select** * **from** yth.etl_tool    
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'
* **select** * **from** yth.etl_tool      
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'ILINE'
* **select** * **from** yth.etl_tool    
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'SPUTTER'
* **select** * **from** yth.etl_tool   
**where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc'  
**and** toolg_id = 'SPUTTER'  
**order by** tool_id, ch_id

## __etl_mask_info__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_mask_info' **order by** update_time **desc** **limit** 100;  
* **select** * **from** yth.etl_mask_info  
**where** parentid = 'e188f944-d0a6-41ca-e053-24017e0a9c9f'  

**1. Find the machine in the position column**     
* **select** * **from** yth.etl_mask_info   
**where** parentid = 'e188f944-d0a6-41ca-e053-24017e0a9c9f'  
**and** **position in** (**select** tool_id **from** yth.etl_tool **where** parentid = 'e188d57e-530b-4ce8-e053-24017e0aabfc')

## __etl_demand__
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_demand' **order by** update_time **desc** **limit** 100;

**1. Key stage demand** 
* **select** * **from** yth.etl_demand   
**where** parentid = 'e188d57c-4426-4cf2-e053-24017e0adc95'  
**and** seq = 1

## __etl_lothistory__
* **select** * **from** yth.etl_demand **where** parentid = 'e188d57c-4426-4cf2-e053-24017e0adc95'  
**and** seq = 3  
* **select** * **from** yth.etl_lothistory   
**where** track_out >= '2022-06-16 07:20'  
**order by** tool_id, track_in  
* **select** * **from** yth.etl_lothistory     
**where** track_out >= '2022-06-16 07:20'    
**and** toolg_id = 'ILINE'  
**order by** tool_id, track_in
* **select** * **from** yth.etl_lothistory   
**where** track_out >= '2022-06-16 07:20'    
**and** toolg_id = 'ILINE'    
**and** stage **in** ('ALZER-Z', 'ALZER', 'ALZER-1')  
**order by** tool_id, track_in
