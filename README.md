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
**Select the newest version of etl_flow**
* **select** * from yth.etl_ver_control **where** **table_name** = 'etl_flow' **order by** update_time **desc** **limit** 100;
## __Search-for-the-specific-parentid__
**Find the specific parentid and order the data by prod_id, plan_no, step_id**
* **select** * from yth.etl_flow **where** parentid = 'e69121eb-55af-04b5-e053-24017e0a9724' **order by** prod_id, plan_no, step_id;
