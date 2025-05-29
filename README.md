📝 Исправление ошибок в тексте с использованием алгоритмов и машинного обучения
🔧 Установка зависимостей
Для работы проекта установите:

bash
Копировать
Редактировать
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

замена буквы

удаление буквы

перестановка букв

добавление лишней буквы

Каждое "неправильное" слово сопоставлено с правильным в датафрейме.

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
Я обучила простую LSTM-модель, которая принимает искажённое слово и предсказывает правильное. Сначала все слова были токенизированы и дополнены паддингом до одинаковой длины.

Архитектура:

Embedding слой

LSTM

Полносвязный Dense выход с softmax

Точность достигла ~100% на синтетических данных уже на 10 эпохе 🥹

python
Копировать
Редактировать
model.fit(sequences_wrong, sequences_right, epochs=10, batch_size=32)
🧪 Демонстрация
Я сделала два небольших виджета (на Jupyter Notebook), где можно вручную ввести слово(а) с ошибкой и увидеть, как:

🔤 Алгоритм Левенштейна исправит текст

🧠 Модель на LSTM даст свою версию исправлений

Оба виджета основаны на ipywidgets и работают прямо в ноутбуке.

📌 Выводы
🔹 Алгоритм Левенштейна быстрее и проще, но работает только на уже известных словах.
🔹 Нейросеть гибче, но требует обучения и больше вычислений.
🔹 У каждого метода свои плюсы, и в зависимости от задачи можно выбрать подходящий.

Если вам понравился проект — ставьте ⭐ и пишите, буду рада обратной связи! 😊
