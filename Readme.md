# Проект: Генерация квестов, диалогов и описание локаций для текстовой игры с использованием RAG
Этот проект был создан для автоматической генерации квестов, диалогов и игровых локаций для текстовых видеоигр. Основной акцент сделан на использовании RAG (Retrieval-Augmented Generation) для создания насыщенного контекста на основе известных литературных произведений.

### Данные для RAG
Для создания базы данных RAG были использованы следующие классические тексты:

1) The Hobbit - Дж.Р.Р. Толкин
2) World War - Герберт Уэльс
3) King Arthur - легенды и мифы о короле Артуре

Эти тексты были обработаны и индексированы с помощью FAISS, что позволяет быстро искать фрагменты текста для подстановки в генеративные запросы.

### Подход к созданию RAG
1. Извлечение и индексирование
Для создания базы данных RAG использовались сырые текстовые файлы, которые были предварительно обработаны для очистки от лишних символов и разбиты на логические фрагменты. Эти фрагменты затем были конвертированы в векторные представления с помощью модели all-MiniLM-L6-v2 из библиотеки sentence-transformers. Итоговый индекс был создан с использованием FAISS.

2. Генерация гипотетических документов (HyDE)
Для каждого запроса создается гипотетический ответ, который используется для поиска релевантных фрагментов в индексе. Этот метод позволяет значительно улучшить качество результатов, так как генератор получает дополнительный контекст перед финальной генерацией.

Пример промпта для HyDE:
```
Imagine a detailed, hypothetical answer to the following question: {question}
```
3. Многовариантные запросы (MultiQuery)
Для увеличения разнообразия ответов используется метод многовариантных запросов, где один запрос преобразуется в несколько альтернативных формулировок, что позволяет охватить больше возможных ответов из базы данных.

Пример промпта для MultiQuery:
```
Generate 5 different ways to ask the following question in a more detailed and creative way: {question}
```
### Примеры запросов и ответы
Пример 1: Создание локации в стиле войны будущего с пришельцами
Запрос:
```
Generate a location in the style of a futuristic war with aliens.
```
Результат:
```
Hypothetical Location: The Battle of Novaya Zemlya

Location Description:

Name: Novaya Zemlya  
Region: Arctic Circle, Siberia  
Environment: A desolate, icy archipelago, where winds howl relentlessly and snow drifts across frozen plains. The landscape is rugged, with jagged mountains, glaciers, and vast stretches of ice-covered tundra.

Key Features:
1. Fortress of Novaya Zemlya - A massive, heavily fortified military base built deep beneath the ice.
2. Alien Outposts - Scattered across the icy plains, equipped with cloaking technology and advanced weaponry.
3. Tundra Battlefields - Frozen plains where intense battles rage between human soldiers and alien forces.
```

Пример 2: Создание диалога в стиле средневековых разговоров
Запрос:

```
Create a dialogue in the style of medieval conversations.
```

Результат:

```
Scene: The Great Hall of the Royal Castle.

King Valdemar the Just: "Hear ye, hear ye, all good people of my realm! It has been many years since we gathered here to discuss the matters of the land. Today, we have important business to attend to. Sir Gawain, tell us what news you have brought from the outer marches?"

Sir Gawain: "Most noble King, peace be upon you. I have ridden far and wide, from the western shores to the eastern plains. There is no great war or plague to trouble us, but we do face a challenge. The villages along the border have been plagued by bandits."

Lady Arianna: "Your majesty, perhaps we should send scouts to gather intelligence on their movements. We must know their habits and patterns before we can plan a proper defense."
```

Пример 3: Создание квеста в стиле фэнтези-путешествия
Запрос:
```
Редактировать
Generate a quest in the style of a fantasy adventure.
```
Результат:
```
The Quest: The Dragon's Hoard of Remembrance

Introduction:

In the distant kingdom of Valdoria, a legendary tale has been whispered for centuries: a dragon named Malador, the “Guardian of the Golden Coast,” has been slain by an unknown hero. His treasure was buried deep beneath the waves, guarded by a powerful enchantment.

Quest Objectives:
1. Discover the location of the dragon’s lair.
2. Retrieve the Key of the Deep, a magical artifact that opens the underwater catacombs.
3. Confront the ghost of Malador and lift the curse of the treasure.
```

Особенности проекта
Автоматическое создание контекста: Использует подход RAG для комбинирования поиска и генерации текста.

Высокая скорость поиска: Использует FAISS для быстрого поиска релевантных документов.

Гибкость генерации: Поддерживает многовариантные запросы для расширения вариантов ответов.

Заключение
Проект позволяет быстро и качественно генерировать сложные текстовые фрагменты для текстовых видеоигр, что значительно упрощает процесс создания квестов и игровых миров.