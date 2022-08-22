# pgAdmin
# Tutorial of pgAdmin
<details open="open">
  <summary><b>Table of Contents</b></summary>
  <ol>
    <li>
      <a href="#introduction">Introduction</a>
    </li>
    <li>
      <a href="#the-gui">The script</a> 
      <ul>
        <li><a href="#select-the-newest-version">Select-the-newest-version</a></li>
        <li><a href="#search-for-the-specific-parentid">Search-for-the-specific-parentid</a></li>  
      </ul>
    </li>
    <li>
      <a href="#the-instructions-for-this-database">The instructions for this database</a>
    </li>
    
  </ol>
</details>

# __Introduction__
This repository is a tutorial for __pgAdmin 4__, including the script for searching some specific data.
# __The script__
## __Select-the-newest-version__
**Select the newest version of etl_flow and extract 100 data**
* **select** * **from** yth.etl_ver_control **where** **table_name** = 'etl_flow' **order by** update_time **desc** **limit** 100;
## __Search-for-the-specific-parentid__
**Find the specific parentid and order the data by prod_id, plan_no, step_id**
* **select** * **from** yth.etl_flow **where** parentid = 'e69121eb-55af-04b5-e053-24017e0a9724' **order by** prod_id, plan_no, step_id;
  
**Just give the number to the data, if the prod_id is the same, then it will give the number in ascending order**
* **select** **row_number()** **over** (**partition by** prod_id **order by** plan_no, step_id) **as** rtn, *  
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

**etl_qtime_spec**
| Column  | Description |
| ------------- | ------------- |
| parentid  | 版本號  |
| prod_id  | Product ID  |
| plan_id  | Process/Plan/Route ID |
| step_id_from | Qtime限制起點站點編號 |
| step_id_to | Qtime限制終點站點編號 |
| timelimit | Qtime限制長度 |
| update_time | 資料更新時間 |

**etl_wip**
| Column  | Description |
| ------------- | ------------- |
| parentid  | 版本號  |
