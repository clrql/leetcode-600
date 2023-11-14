
  # immediate-food-delivery-i

  ```pythondata
  def food_delivery(delivery: pd.DataFrame) -> pd.DataFrame:
    immediate_orders = delivery[delivery['order_date'] == delivery['customer_pref_delivery_date']]
    total_orders = len(delivery)
    immediate_count = len(immediate_orders)
    immediate_percentage = (immediate_count / total_orders) * 100
    
    result = pd.DataFrame({'immediate_percentage': [round(immediate_percentage, 2)]})
    return result
  ```
  