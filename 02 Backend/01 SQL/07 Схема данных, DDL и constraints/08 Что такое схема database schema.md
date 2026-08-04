# Что такое схема database schema?

> [!NOTE]
> Слово schema может означать структуру базы данных в целом или namespace внутри базы, который группирует таблицы и другие объекты. Важно понимать оба значения.

## Schema как структура

Когда говорят "схема БД", часто имеют в виду модель:

- таблицы;
- колонки;
- типы;
- ключи;
- индексы;
- constraints;
- связи.

## Schema как namespace

В PostgreSQL schema - это пространство имен.

```sql
CREATE SCHEMA billing;

CREATE TABLE billing.invoices (
  id bigint PRIMARY KEY,
  total numeric(10, 2) NOT NULL
);
```

Теперь таблица называется `billing.invoices`.

## Зачем namespaces?

- разделение доменов;
- изоляция объектов;
- управление доступами;
- организация больших баз;
- разделение internal/public объектов.

## Мини-шпаргалка

- Schema может означать модель данных.
- В PostgreSQL schema - namespace внутри базы.
- Таблицу можно указывать как `schema.table`.
- Namespaces помогают организовать большие системы.
- Не путай schema и database instance.
