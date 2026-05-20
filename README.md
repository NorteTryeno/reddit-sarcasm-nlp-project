# Sarcasm Detection in Reddit Comments

Проект по определению сарказма в комментариях Reddit.

В рамках проекта были реализованы:

- baseline-модель на TF-IDF + Logistic Regression
- подход на основе BERT
- анализ ошибок моделей и ограничений задачи

Датасет:
https://www.kaggle.com/datasets/danofer/sarcasm

---

## Структура проекта

- Sarcasm.ipynb (TF-IDF + Logistic Regression)
- bert_sarcasm_detection.ipynb (BERT fine-tuning)
- README.md
- requirements.txt

---

## Результаты

| Модель                       | Accuracy | F1-score |
| ---------------------------- | -------- | -------- |
| TF-IDF + Logistic Regression | 0.6939   | 0.6833   |
| BERT                         | 0.7162   | 0.7026   |

---

# Sarcasm.ipynb

Baseline-проект на основе classical NLP.

Используемые подходы:

- TF-IDF vectorization
- Logistic Regression
- n-grams
- расширение пространства признаков (`max_features`)

---

## Предобработка данных

В проекте выполняется:

- очистка текста
- удаление пустых строк
- анализ длины комментариев
- приведение текста к нижнему регистру

---

## Эксперименты

Проводились эксперименты с:

- baseline TF-IDF
- n-граммами
- увеличением `max_features`

---

## Результаты baseline

| Конфигурация              | F1-score |
| ------------------------- | -------- |
| Baseline TF-IDF           | 0.6687   |
| + n-grams                 | 0.6805   |
| + увеличение max_features | 0.6833   |

---

# bert_sarcasm_detection.ipynb

Продолжение проекта с использованием BERT.

Используемые технологии:

- HuggingFace Transformers
- PyTorch
- BERT fine-tuning

---

## Подготовка данных

На этапе подготовки:

- тексты токенизируются через BERT tokenizer
- создаются `input_ids` и `attention_mask`
- данные переводятся в формат PyTorch tensors

---

## Fine-tuning

Используется модель:

```python
bert-base-uncased
```

Обучение выполнялось на задаче бинарной классификации:

- sarcasm
- non-sarcasm

---

## Результаты BERT

| Модель | Accuracy | F1-score |
| ------ | -------- | -------- |
| BERT   | 0.7162   | 0.7026   |

---

## Анализ ошибок

Во время анализа ошибок удалось заметить несколько особенностей:

- BERT лучше справляется с короткими и более естественными комментариями
- TF-IDF сильнее опирается на поверхностные паттерны
- обе модели ограничены отсутствием диалогового контекста

Некоторые комментарии невозможно корректно интерпретировать без `parent_comment`.

Например:

_so accurate_

или:

_various bugs have been fixed stability improvements_

Без контекста такие сообщения могут выглядеть как обычные комментарии, хотя в рамках диалога являются сарказмом.

---

## Ограничения проекта

Текущие модели:

- не используют `parent_comment`
- не учитывают структуру диалога
- работают только с текстом самого комментария

---

## Возможные улучшения

Потенциальные направления развития:

- использование `parent_comment`
- context-aware sarcasm detection
- multi-input transformer models

---

## Как запустить проект

1. Скачать датасет с Kaggle
2. Поместить `.csv` файл в папку `data/`
3. Установить зависимости:

```bash
pip install -r requirements.txt
```

4. Запустить:

- `Sarcasm.ipynb`
- `bert_sarcasm_detection.ipynb`
