
  # sales-person

  ```pythondata
  import pandas as pd

def sales_person(sales_person: pd.DataFrame, company: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:
    # Merge the SalesPerson and Orders tables on 'sales_id'
    merged = sales_person.merge(orders, on='sales_id', how='left')
    
    # Merge the merged DataFrame with the Company table on 'com_id'
    merged = merged.merge(company, on='com_id', how='left')
    
    # Filter the DataFrame to include only rows where company name is 'RED'
    red_orders = merged[merged['name_y'] == 'RED']
    
    # Find the salespersons who have orders related to company 'RED'
    salespersons_with_red_orders = red_orders['sales_id'].unique()
    
    # Filter the original SalesPerson DataFrame to exclude those with red orders
    result = sales_person[~sales_person['sales_id'].isin(salespersons_with_red_orders)]
    
    # Select and return only the 'name' column
    result = result[['name']]
    
    return result
  ```
  