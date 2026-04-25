[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/kOqwghv0)
# ML Project — Аналитика подозрительных компаний

**Студент:** Булгаков Егор Александрович

**Группа:** БИВ231

## Оглавление

1. [Описание проекта](#описание-проекта)
2. [Структура репозитория](#структура-репозитория)
3. [Быстрый старт](#быстрый-старт)
4. [Данные](#данные)
5. [Результаты](#результаты)
6. [Артефакты](#артефакты)
7. [Отчёт](#отчёт)

## Описание проекта

Проект посвящён выявлению подозрительных компаний по финансовым, поведенческим и связанным с бенефициарами признакам.

В текущей реализации анализ выполняется в ноутбуке `notebooks/analytica.ipynb` и включает:

- генерацию синтетического тестового датасета с пометкой fraud / non-fraud;
- разведочный анализ данных и временных срезов;
- feature engineering на уровне компании;
- rule-based fraud scoring;
- unsupervised anomaly detection с помощью Isolation Forest, LOF и DBSCAN;
- объединение сигналов в итоговый `composite_score`;
- экспорт итоговых CSV в папку `data/processed`.

Цель проекта: построить воспроизводимый антифрод-пайплайн, который позволяет ранжировать компании по уровню риска и объяснять причины попадания в список подозрительных.

## Структура репозитория

```text
.
├── data
│   ├── processed              # Результаты анализа и экспортированные CSV
│   └── raw                    # Исходные и тестовые CSV
├── models                     # Папка под сохранённые модели
├── notebooks
│   └── analytica.ipynb        # Основной ноутбук с антифрод-аналитикой
├── presentation
│   └── README.md              # Материалы для презентации
├── report
│   └── report.md              # Текст отчёта
├── src
│   └── __init__.py
├── tests
│   └── test.py
├── requirements.txt
└── README.md
```

## Быстрый старт

```bash
# 1. Клонировать репозиторий
git clone <url>
cd hseml-group-project-gorg1t

# 2. Создать виртуальное окружение
python -m venv .venv

# 3. Активировать окружение
# Windows
.venv\Scripts\activate

# Linux / macOS
source .venv/bin/activate

# 4. Установить зависимости
pip install -r requirements.txt
```

После установки зависимостей откройте `notebooks/analytica.ipynb` и выполните ячейки последовательно.

## Данные

В проекте используется следующая схема хранения CSV:

- `data/raw/test_data.csv` — синтетический набор данных для запуска ноутбука;
- `data/raw/test_gt.csv` — ground truth для проверки качества на синтетике;
- `data/processed/fraud_scores_all.csv` — скоринг по всем компаниям;
- `data/processed/suspicious_companies.csv` — итоговый список подозрительных компаний.

Ноутбук уже настроен так, чтобы чтение CSV происходило из `data/raw`, а сохранение результатов — в `data/processed`.

## Результаты

По текущему сохранённому прогону ноутбука:

- проанализировано 120 компаний;
- в итоговый список подозрительных попали 34 компании;
- распределение по уровням риска: 18 `CRITICAL`, 3 `HIGH`, 13 `MEDIUM`, 86 `LOW`.

Используемые методы детекции:

- rule-based scoring;
- Isolation Forest;
- Local Outlier Factor;
- DBSCAN;
- composite scoring поверх нескольких сигналов.

## Артефакты

Основные выходные файлы после запуска ноутбука:

- `data/raw/test_data.csv`
- `data/raw/test_gt.csv`
- `data/processed/fraud_scores_all.csv`
- `data/processed/suspicious_companies.csv`

## Отчёт

Финальный отчёт: [`report/report.md`](report/report.md)
