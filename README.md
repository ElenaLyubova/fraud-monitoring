# fraud-monitoring
# ETL Процесс для Обработки Данных

## Описание задачи

Разработка ETL процесса, который получает ежедневные выгрузки данных, загружает их в хранилище и строит отчеты по мошенническим операциям.

## Выгрузка данных

Каждый день загружаются следующие файлы:
- **Транзакции** (CSV)
- **Терминалы** (XLSX)
- **Черный список паспортов** (XLSX)

## Структура хранилища

Данные загружаются в хранилище с полями для отслеживания версий (SCD1 и SCD2).

## Построение отчета

Ежедневно строится витрина по мошенническим операциям с полями:
- `event_dt`
- `passport`
- `fio`
- `phone`
- `event_type`
- `report_dt`

### Признаки мошенничества

1. Операции с просроченными или заблокированными паспортами.
2. Операции с недействительными договорами.
3. Операции в разных городах в течение часа.
4. Попытки подбора суммы в течение 20 минут.

## Правила именования таблиц

- `STG_<TABLE_NAME>` — Стейджинговые таблицы.
- `DWH_FACT_<TABLE_NAME>` — Таблицы фактов.
- `DWH_DIM_<TABLE_NAME>` — Таблицы измерений SCD1.
- `REP_FRAUD` — Таблица с отчетом.

## Обработка файлов

Файлы именуются по шаблону:
- `transactions_DDMMYYYY.txt`
- `passport_blacklist_DDMMYYYY.xlsx`
- `terminals_DDMMYYYY.xlsx`

После обработки файлы переименовываются и перемещаются в каталог `archive`.

