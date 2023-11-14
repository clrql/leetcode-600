
  # actors-and-directors-who-cooperated-at-least-three-times

  ```pythondata
  import pandas as pd

def actors_and_directors(actor_director: pd.DataFrame) -> pd.DataFrame:
    # Group by actor_id and director_id, then count the occurrences
    counts = actor_director.groupby(['actor_id', 'director_id']).size().reset_index(name='count')
    
    # Filter the pairs that have a count of at least three
    result = counts[counts['count'] >= 3][['actor_id', 'director_id']]
    
    return result

  ```
  