
  # find-total-time-spent-by-each-employee

  ```pythondata
  import pandas as pd

def total_time(employees: pd.DataFrame) -> pd.DataFrame:
    # Calculate the total time spent by each employee on each day
    employees['total_time'] = employees['out_time'] - employees['in_time']
    
    # Group by 'event_day' and 'emp_id', then sum the total_time for each group
    result = employees.groupby(['event_day', 'emp_id'])['total_time'].sum().reset_index()
    
    # Rename columns for the output
    result.columns = ['day', 'emp_id', 'total_time']
    
    return result
  ```
  