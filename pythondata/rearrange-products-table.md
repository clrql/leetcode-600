
  # rearrange-products-table

  ```pythondata
  import pandas as pd

def rearrange_products_table(products: pd.DataFrame) -> pd.DataFrame:
    store_columns = products.columns[1:]  # Get the store columns
    rows = []
    
    for index, row in products.iterrows():
        for store_col in store_columns:
            if pd.notna(row[store_col]):
                rows.append([row['product_id'], store_col, row[store_col]])
    
    result = pd.DataFrame(rows, columns=['product_id', 'store', 'price'])
    return result
  ```
  