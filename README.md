# DS_Tweet

Multiclass tweet sentiment analysis comparing NLP preprocessing, vectorization and classification approaches. Best model: TF-IDF + Logistic Regression, ROC-AUC 0.9784.

---

# Tweet Sentiment Analysis

Multiclass sentiment classification of tweets into **negative, neutral and positive** classes.

The project explores how different text preprocessing and vectorization strategies affect classification quality and compares several classical machine learning algorithms for sparse NLP data.

## Overview

The dataset contains **3,865 tweets** divided into three sentiment classes:

* Negative — 1,116
* Neutral — 1,566
* Positive — 1,183

The data was split into train and test sets using an **80/20 stratified split**.

The main goal was not only to train a classifier, but to systematically compare different NLP pipelines.

## Approach

### Text preprocessing

Six preprocessing strategies were compared:

* tokenization
* stemming
* lemmatization
* stemming + spelling correction
* lemmatization + spelling correction
* stemming + stopword removal

### Vectorization

Each preprocessing strategy was combined with three text representations:

* Binary Bag of Words
* Count Bag of Words
* TF-IDF

This resulted in **18 different text representations**.

### Models

Three classifiers were trained for every representation:

* Logistic Regression
* Linear SVC
* Multinomial Naive Bayes

In total, **54 model configurations** were evaluated.

Cosine similarity was also calculated for all 18 text representations to explore how different NLP transformations affect similarity between tweets.

## Results

The best-performing configuration was:

**Tokenization + TF-IDF + Logistic Regression**

| Metric                       | Result |
| ---------------------------- | -----: |
| Test Accuracy                | 0.8926 |
| Test ROC-AUC                 | 0.9784 |
| Best Logistic Regression `C` |      1 |

`GridSearchCV` with 5-fold cross-validation was used to tune the regularization parameter of the final Logistic Regression model.

An interesting result was that more aggressive preprocessing did not improve performance: simple tokenization preserved useful information better than stemming or lemmatization in the best-performing pipeline.

## Tech Stack

* Python
* pandas
* NumPy
* NLTK
* scikit-learn
* pyspellchecker
* Jupyter Notebook

## Data

The source dataset is not included in this repository.

The notebook expects the following files inside the `datasets/` directory:

```text
datasets/
├── processedPositive.csv
├── processedNegative.csv
└── processedNeutral.csv
```

Class labels used in the project:

```text
0 — negative
1 — neutral
2 — positive
```

## Running the Project

Install the main dependencies:

```bash
pip install pandas numpy nltk scikit-learn pyspellchecker jupyter
```

Place the dataset files in `datasets/` and run the notebook from Jupyter.

## Notes

The original CSV files have an unusual structure: natural commas inside tweet text are not consistently quoted, which makes perfect reconstruction of some original records impossible.

The loader therefore follows the physical structure of the provided files. This is treated as a limitation of the source data rather than silently corrected 


___________________________________________________________________________________________________________________________________________________________________


# Tweets Sentiment Analysis — русский README

Многоклассовый анализ тональности твитов с сравнением различных подходов к предобработке текста, векторизации и классификации. Лучшая модель: TF-IDF + Logistic Regression, ROC-AUC 0.9784.

---

# Анализ тональности твитов

Проект по многоклассовой классификации твитов на три категории: **негативные, нейтральные и позитивные**.

Основная цель проекта — не просто обучить классификатор, а системно сравнить различные подходы к предобработке текста, векторизации и машинному обучению.

## Данные

Датасет содержит **3 865 твитов**:

* Negative — 1 116
* Neutral — 1 566
* Positive — 1 183

Данные были разделены на train и test в пропорции **80/20** с сохранением долей классов с помощью stratification.

## Подход

### Предобработка текста

Было протестировано шесть вариантов:

* tokenization
* stemming
* lemmatization
* stemming + исправление опечаток
* lemmatization + исправление опечаток
* stemming + удаление stopwords

### Векторизация

Каждый вариант предобработки был объединён с тремя способами представления текста:

* Binary Bag of Words
* Count Bag of Words
* TF-IDF

В результате было сформировано **18 вариантов представления данных**.

### Модели

На каждом из 18 наборов признаков были обучены три классификатора:

* Logistic Regression
* Linear SVC
* Multinomial Naive Bayes

Всего было проведено **54 ML-эксперимента**.

Также для всех 18 представлений рассчитывалась cosine similarity, чтобы сравнить влияние разных способов обработки текста на близость твитов.

## Результаты

Лучшей комбинацией стала:

**Tokenization + TF-IDF + Logistic Regression**

| Метрика             | Результат |
| ------------------- | --------: |
| Test Accuracy       |    0.8926 |
| Test ROC-AUC        |    0.9784 |
| Лучший параметр `C` |         1 |

Для подбора параметра регуляризации финальной Logistic Regression использовался `GridSearchCV` с 5-fold cross-validation.

Интересный результат проекта: более агрессивная обработка текста не улучшила качество. В данном датасете простая токенизация сохранила больше полезной информации, чем stemming или lemmatization.

## Стек

* Python
* pandas
* NumPy
* NLTK
* scikit-learn
* pyspellchecker
* Jupyter Notebook

## Датасет

Исходные данные не включены в репозиторий.

Ноутбук ожидает следующую структуру:

```text
datasets/
├── processedPositive.csv
├── processedNegative.csv
└── processedNeutral.csv
```

Используемые метки классов:

```text
0 — negative
1 — neutral
2 — positive
```

## Запуск

Установите основные зависимости:

```bash
pip install pandas numpy nltk scikit-learn pyspellchecker jupyter
```

Поместите исходные CSV-файлы в папку `datasets/` и запустите ноутбук через Jupyter.

## Ограничения данных

Исходные CSV-файлы имеют нестандартную структуру: естественные запятые внутри текста не всегда экранированы кавычками.

Из-за этого для некоторых фрагментов невозможно однозначно определить, является ли запятая частью текста или разделителем между записями.

Используемый loader следует физической структуре предоставленных файлов. Это рассматривается как ограничение исходных данных.
during preprocessing.

