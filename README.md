# 📝 Исправление ошибок в тексте с использованием алгоритмов и машинного обучения

---

## 🔧 Установка зависимостей

Для работы проекта установите:

```bash
pip install Levenshtein
Также используются библиотеки:

python
Копировать
Редактировать
import pandas as pd
import numpy as np
import tensorflow as tf
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.layers import Input, Embedding, LSTM, Dense
from tensorflow.keras.models import Model
📚 Данные
Я взяла 10 000 русских слов из словаря (dict.txt) и сгенерировала к ним искажённые варианты, используя простую функцию с четырьмя типами ошибок:

🔄 замена буквы

❌ удаление буквы

🔁 перестановка букв

➕ добавление лишней буквы

Каждое "неправильное" слово сопоставлено с правильным в DataFrame.

🔍 Подход №1 — Алгоритм Левенштейна
Используется библиотека Levenshtein, которая находит наиболее близкое по расстоянию слово из словаря:

python
Копировать
Редактировать
def correct_word(word, dictionary):
    min_distance = float('inf')
    corrected_word = None
    for correct_word in dictionary:
        distance = Levenshtein.distance(word, correct_word)
        if distance < min_distance:
            min_distance = distance
            corrected_word = correct_word
    return corrected_word
🤖 Подход №2 — Нейросеть (LSTM)
Я обучила простую LSTM-модель, которая принимает искажённое слово и предсказывает правильное.

Подготовка данных:
Все слова токенизировались и дополнялись паддингом до одинаковой длины.

Архитектура модели:

📥 Embedding слой

🧠 LSTM

🧾 Полносвязный Dense-выход с softmax

Точность достигла ~100% на синтетических данных уже на 10-й эпохе 🥹

Пример обучения:

python
Копировать
Редактировать
model.fit(sequences_wrong, sequences_right, epochs=10, batch_size=32)
🧪 Демонстрация
Сделала два небольших виджета (на Jupyter Notebook), где можно вручную ввести слово(а) с ошибкой и увидеть, как:

🔤 Алгоритм Левенштейна исправляет текст

🧠 Модель на LSTM предлагает своё исправление

Оба виджета основаны на ipywidgets и работают прямо в ноутбуке.

📌 Выводы
🔹 Алгоритм Левенштейна — быстрее и проще, но работает только на уже известных словах

🔹 Нейросеть — гибче и мощнее, но требует обучения и ресурсов

🔹 У каждого метода есть свои плюсы — выбирайте подход под задачу

Если вам понравился проект — ставьте ⭐ и пишите!
Буду рада обратной связи 😊
