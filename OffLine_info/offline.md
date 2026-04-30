# Памятка: как поставить Python-библиотеки без интернета

Если на компьютере отключён интернет, библиотеки можно скачать заранее.

---

## Вариант 1 — лучший: скачать все зависимости из `requirements.txt`

На компьютере **с интернетом**:

```bash
pip freeze > requirements.txt
mkdir OffLine_libs
pip download -r requirements.txt -d OffLine_libs
```

В итоге появятся:

```text
requirements.txt
OffLine_libs/
```

Их нужно скопировать на рабочий компьютер без интернета.

На рабочем компьютере:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install --no-index --find-links=OffLine_libs -r requirements.txt
```

Что значат параметры:

```text
--no-index              не ходить в интернет
--find-links=OffLine_libs искать пакеты в локальной папке
```

---

## Вариант 2 — скачать конкретные библиотеки

На компьютере **с интернетом**:

```bash
mkdir OffLine_libs
pip download pandas geopandas matplotlib shapely pyogrio pyproj -d OffLine_libs
```

Потом перенести папку `OffLine_libs` на рабочий компьютер.

На рабочем компьютере:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install --no-index --find-links=OffLine_libs pandas geopandas matplotlib shapely pyogrio pyproj
```

Для работы с GeoPandas можно заранее скачать такой набор:

```bash
pip download geopandas matplotlib pyogrio shapely pyproj fiona -d OffLine_libs
```
