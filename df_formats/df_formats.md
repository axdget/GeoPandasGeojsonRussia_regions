# Форматы для сохранения DataFrame и GeoDataFrame


**Parquet** — это современный файловый формат для таблиц, типа «умный CSV», только:
Появился в **2013 году**, активно используется в аналитике, Big Data, pandas, Spark, DuckDB, Polars.
```python
#pip install pyarrow
import pandas as pd

df = pd.DataFrame({
    "name": ["Иван", "Анна", "Олег"],
    "age": [25, 31, 40],
    "salary": [70000.5, 85000.0, 92000.75]
})

# сохранить
df.to_parquet("people.parquet")

# прочитать обратно
df2 = pd.read_parquet("people.parquet")

print(df2)
print(df2.dtypes)
```

---

`pickle` — это формат Python, который сохраняет объект почти «как есть».

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["Иван", "Анна"],
    "age": [25, 31]
})

# сохранить
df.to_pickle("people.pkl")

# прочитать
df2 = pd.read_pickle("people.pkl")

print(df2)
```

Но `pickle` — это формат **только для Python**.

Важный момент: **нельзя открывать чужие `.pkl` файлы**, потому что внутри может быть вредный код.

---

`GPKG` — это **GeoPackage**, формат именно для геоданных: районы, полигоны, точки, линии, карты.

Для GeoPandas:

```python
import geopandas as gpd

gdf = gpd.read_file("KrasnodarskKrayRayony.GeoJSON")

# сохранить в GeoPackage
gdf.to_file("rayony.gpkg", driver="GPKG")

# прочитать обратно
gdf2 = gpd.read_file("rayony.gpkg")

print(gdf2.head())
```

`gpkg` удобнее, чем `geojson`, если геоданных много. Он компактнее, надёжнее и может хранить несколько слоёв в одном файле.

Например:

```python
gdf.to_file("krasnodar.gpkg", layer="rayony", driver="GPKG")
```

Потом читаешь конкретный слой:

```python
gdf = gpd.read_file("krasnodar.gpkg", layer="rayony")
```

---

## Краткое сравнение

| Формат | Для чего |
|---|---|
| `csv` | простая таблица, но без нормального хранения типов |
| `parquet` | хороший современный формат для таблиц |
| `pickle` | сохранить Python-объект как есть |
| `geojson` | обмен геоданными, удобно смотреть как текст |
| `gpkg` | хороший формат для серьёзных геоданных |
