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
        <li><a href="#select-the-newest-version">Select the newest version</a></li>
        <li><a href="#search-for-the-specific-parentid">Search for the specific parentid</a></li>  
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
| process_time | 製程處理時間 = Track Out Time–Track In Time (單位：小時) |
| cycle_time | 站點週期時間 = Track Out Time–Arrival Time (單位：小時) |
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

# __The script__
## __Select the newest version__
**Select the newest version of etl_flow and extract 100 data**
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_flow' **order by** update_time **desc** **limit** 100;
## __Search for the specific parentid__
**Find the specific parentid and order the data by prod_id, plan_no, step_id**
* **select** * **from** yth.etl_flow **where** parentid = 'e69121eb-55af-04b5-e053-24017e0a9724' **order by** prod_id, plan_no, step_id;
  
**Just give the number to the data, if the prod_id is the same, then it will give the number in ascending order**
* **select**   
	**row_number()** **over** (**partition by** prod_id **order by** plan_no, step_id) **as** rtn, *  
**from** yth.etl_flow;  
**where** parentid = 'e17f9d53-1e23-141f-e053-24017e0a7d15'  
**order by** prod_id, plan_no, step_id  
**limit** 1000;  

* **select** * **from** yth.etl_flow **limit** 100;
* **select**  
	**row_number()** **over**(**partition by** prod_id **order by** plan_no, step_id)**as** rtn, *  
**from** yth.etl_flow  
**where** parentid = 'c7d78df4-91d6-517f-e053-24017e0a85af' **and** prod_id='VP4611F-TBR1HAZ1.02'  
**order by** prod_id, plan_no, step_id

Note: Different prod_id has differnt groups of numbers


