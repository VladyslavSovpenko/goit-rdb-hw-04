# goit-rdb-hw-04 — DML/DDL та складні SQL-вирази на Olist

## Датасет

**Brazilian E-Commerce Public Dataset by Olist** — https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
~100 тис. замовлень бразильського маркетплейсу (2016–2018). Використано 6 файлів: customers, orders, order_items, products, sellers, order_reviews.

## Отримання даних

- **Варіант A (у ноутбуці за замовчуванням, якщо CSV не знайдено локально):** `kagglehub.dataset_download('olistbr/brazilian-ecommerce')` — для публічного датасету облікові дані Kaggle не потрібні.
- **Варіант B:** ті самі 6 CSV лежать у репозиторії в `data/olist/` (56 МБ). Ноутбук спочатку шукає їх там, тому в Colab достатньо `git clone` репозиторію.

Raw-таблиці `olist_*_raw` завантажуються через `pandas.to_sql`, потім дані переносяться в typed-схему (`INSERT ... SELECT` з приведенням типів) за DDL з умови.

## Зміст

| Файл | Що це |
|---|---|
| `notebooks/hw4_olist_dml_joins.ipynb` | ноутбук з output: setup + typed-схема, 4 DML-запити (RETURNING, ON CONFLICT, UPDATE FROM, DELETE RETURNING), `customer_segments`, 5 JOIN-запитів з інтерпретацією, 3 агрегати з HAVING/STRING_AGG, set operations, window functions, reflection |
| `data/olist/*.csv` | 6 CSV Olist |

## Як запустити

**Google Colab:** клонувати репозиторій (`!git clone https://github.com/VladyslavSovpenko/goit-rdb-hw-04 && cd goit-rdb-hw-04`), відкрити ноутбук, *Runtime → Restart and run all*. PostgreSQL 16 стартує через `pgserver` (`/tmp/hw4_pg`).

**Локально з власним PostgreSQL 16** (наприклад, Docker `postgres:16`):

```bash
export HW4_PG_URI='postgresql+psycopg2://user:password@localhost:5432/dbname'
jupyter notebook notebooks/hw4_olist_dml_joins.ipynb
```
