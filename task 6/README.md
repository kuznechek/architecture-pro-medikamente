# Задание 6. Классификация данных

## Classification Engine

**Classification Engine** - движок для классификации данных перед их загрузкой в хранилище.

- Получение схемы из Schema Registry
- Применение правил к полям
- Простановка тегов: `PUBLIC`, `MEDICAL_SECRET`, `FINANCIAL`, `PII_HASH`
- Отправка метрик

## Слои в ClickHouse

| Слой | Содержимое | Доступ |
|------|------------|--------|
| Raw | Исходные сообщения (аномизированные) | Только ETL |
| Cleansed | Данные после валидации + справочники | Аналитики |s
| Confidential | Записи с тегом `MEDICAL_SECRET` | Аудит  |
| Aggregates | Агрегированные отчёты | Аналитики |
| Audit | Логи доступа ко всем слоям | Админ безопасности |

![to_be.png](https://github.com/kuznechek/architecture-pro-medikamente/blob/feature/task%204/to_be.png)

[to_be.drawio](https://github.com/kuznechek/architecture-pro-medikamente/blob/feature/task%204/to_be.drawio)

## Метрики эффективности классификации

| Метрика | Цель |
|---------|-----|
| Precision (по каждому классу) | Минимум ложных срабатываний |
| Recall (по каждому классу) | Не пропустить конфиденциальные данные |
| F1-мера | Общее качество |
| Throughput | Кол-во сообщений в 1 сек |
