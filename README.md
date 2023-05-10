# plsql-entrega

## 1
---

 CREATE OR REPLACE FUNCTION get_num_employees() 
  RETURNS void 
  DECLARE 
      id_dep departments.department_id%TYPE; 
      num_emp INT; 
      emplo_cur CURSOR (cur_dep_id departments.department_id%TYPE) FOR 
          SELECT COUNT(*) FROM employees WHERE department_id=cur_dep_id; 
      
  BEGIN 
      codigo:=10; 
      OPEN emplo_cur(id_dep); 
      FETCH emplo_cur INTO num_emple; 
      RAISE NOTICE 'numero de empleados de % es %', id_dep, num_emp; 
      
      
  END;

---

## 2
---
 DO 
  BEGIN
      FOR EMPLOYEES IN (SELECT * FROM EMPLOYEES WHERE JOB_ID = 'ST_CLERK') LOOP
          RAISE NOTICE '%', EMPLOYEES.FIRST_NAME;
      END LOOP;
  END;
---

## 3
---
  CREATE OR REPLACE PROCEDURE emp_update_salary() 
  
  DECLARE 
      cur_emp CURSOR FOR (SELECT * FROM Employees) FOR UPDATE; 
      emp Employees%ROWTYPE;
  BEGIN 
      FOR emp IN cur_emp LOOP 
          IF emp.SALARY > 8000 THEN 
              UPDATE Employees SET SALARY=SALARY*1.02 WHERE CURRENT OF cur_emp; 
          ELSE 
              UPDATE Employees SET SALARY=SALARY*1.03 WHERE CURRENT OF cur_emp; 
          END IF; 
      END LOOP; 
      CLOSE cur_emp
  END;
---

