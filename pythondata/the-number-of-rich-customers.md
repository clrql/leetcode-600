
  # the-number-of-rich-customers

  ```pythondata
  import pandas as pd

def count_rich_customers(store: pd.DataFrame) -> pd.DataFrame:
    rich_count = len(store[store['amount'] > 500]['customer_id'].unique())
    result = pd.DataFrame({'rich_count': [rich_count]})
    return result
  ```
  