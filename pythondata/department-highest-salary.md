
  # department-highest-salary

  ```pythondata
  import pandas as pd

def department_highest_salary(employee: pd.DataFrame, department: pd.DataFrame) -> pd.DataFrame:
    merged = pd.merge(employee, department, left_on='departmentId', right_on='id')
    grouped = merged.groupby('name_y').apply(lambda x: x[x['salary'] == x['salary'].max()])
    result = grouped[['name_y', 'name_x', 'salary']].rename(columns={'name_y': 'Department', 'name_x': 'Employee'})
    return result

  ```
  