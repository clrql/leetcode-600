
  # calculate-special-bonus

  ```pythondata
  import pandas as pd

def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:
    # Apply the bonus calculation based on conditions
    employees['bonus'] = employees.apply(lambda row: row['salary'] if row['employee_id'] % 2 == 1 and row['name'][0] != 'M' else 0, axis=1)
    
    # Select and return the 'employee_id' and 'bonus' columns, ordered by 'employee_id'
    result = employees[['employee_id', 'bonus']].sort_values(by='employee_id')
    
    return result

  ```
  