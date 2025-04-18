
# Звіт про виконання лабораторної роботи

**Тема:** Робота з віртуальними середовищами та сторонніми бібліотеками у Python  
**Мета:** Закріпити навички встановлення та використання зовнішніх бібліотек у Python, ознайомитися з інструментами керування середовищами (venv, Pipenv, Poetry) та попрактикуватися у використанні API для отримання зовнішніх даних.

---

## Хід роботи

### Завдання 1. Знайомство з PIP та бібліотекою `requests`

1. **Перевірка роботи менеджера пакетів PIP:**

   Для перевірки встановлення PIP було виконано таку команду в терміналі:

   ```bash
   pip -V
   ```

   У відповідь була виведена версія пакету та шлях його розташування:

   ```
   pip 25.0.1 from C:\Users\Traxinator\AppData\Local\Programs\Python\Python313\Lib\site-packages\pip (python 3.13)
   ```

   Також переглянуто документацію за допомогою:

   ```bash
   pip --help
   ```

2. **Встановлення пакету `requests`:**

   Оскільки бібліотека вже була інстальована раніше, система повідомила:

   ```bash
   pip install requests
   ```

   ```
   Requirement already satisfied: requests in ...
   ```

   Під час спроби використати бібліотеку в інтерпретаторі Python була допущена синтаксична помилка:

   ❌ **Помилковий ввід:**

   ```python
   import request
   response = request.get("https://httpbin.org/get")
   ```

   ✅ **Правильний варіант:**

   ```python
   import requests
   response = requests.get("https://httpbin.org/get")
   print(response.text)
   ```

3. **Робота з методом `iter_lines()`:**

   Для обробки рядків відповіді сервера використано:

   ```python
   import requests

   response = requests.get("https://httpbin.org/stream/5", stream=True)

   for line in response.iter_lines():
       if line:
           print(line.decode('utf-8'))
   ```

4. **Інші команди для управління бібліотекою:**

   ```bash
   pip show requests
   pip install requests==2.1
   pip uninstall requests
   ```

---

### Завдання 2. Бібліотека `jikanpy` та API MyAnimeList

1. **Отримання інформації про аніме:**

   Було використано бібліотеку `jikanpy`, яка дозволяє отримувати інформацію з MyAnimeList через API.

   Встановлення:

   ```bash
   pip install jikanpy
   ```

   Код для отримання списку епізодів аніме (ID 54595):

   ```python
   from jikanpy import Jikan

   jikan = Jikan()
   episodes = jikan.anime(54595, extension='episodes')
   for ep in episodes['episodes']:
       print(ep['episode_id'], ep['title'])
   ```

---

### Завдання 3. Створення віртуального середовища через `venv`

1. **Процедура створення та активації:**

   ```bash
   python -m venv my_env
   my_env\Scripts\activate
   pip install requests
   deactivate
   ```

   Після деактивації перевірено, що пакет `requests` був інстальований лише у глобальному середовищі:

   ```bash
   pip show requests
   ```

---

### Завдання 4. Керування проєктом за допомогою Pipenv

1. **Інсталяція та використання Pipenv:**

   ```bash
   pip install pipenv
   pipenv --python 3.10
   pipenv install requests
   ```

   Pipenv автоматично створює файли `Pipfile` та `Pipfile.lock`.  

2. **Запуск скрипта в цьому середовищі:**

   ```bash
   pipenv run python app3.py
   ```

---

### Завдання 5. Використання змінних середовища з `.env`

1. **Створення `.env` файлу:**

   Файл `.env` містив наступне:

   ```
   HELLO=Привіт світ!
   ```

   Код для роботи з цим файлом:

   ```python
   import os
   from dotenv import load_dotenv

   load_dotenv()

   hello = os.getenv("HELLO")

   if hello:
       print(hello)
   else:
       raise EnvironmentError("Змінна HELLO не знайдена")
   ```

---

### Завдання 6. Використання Poetry

1. **Інсталяція Poetry та створення нового проєкту:**

   ```bash
   poetry new myproject
   cd myproject
   poetry add requests
   poetry show --tree
   ```

2. **Запуск Flask-програми в середовищі Poetry:**

   Створено просту програму на Flask:

   `app.py`

   ```python
   from flask import Flask

   app = Flask(__name__)

   @app.route("/")
   def home():
       return "Це мій Flask-додаток, запущений через Poetry!"

   if __name__ == "__main__":
       app.run(debug=True)
   ```

   Запуск:

   ```bash
   poetry run python app.py
   ```

---

## Висновки

🔹 **Що було виконано:**  
Опановано встановлення та використання бібліотек `requests`, `jikanpy`, створено кілька програм для взаємодії з API, а також освоєно роботу з трьома популярними інструментами створення віртуального середовища.

🎯 **Досягнення мети:**  
Мета роботи виконана повністю — вдалося навчитись ефективно керувати пакетами та середовищами.

📘 **Нові знання:**  
- Створення `.env` файлів та їхнє підключення  
- Порівняння Pipenv та Poetry  
- Робота зі сторонніми API

❗ **Складнощі:**  
Помилка на початку через неправильне ім'я модуля `requests`.

📄 **Оформлення звіту:**  
Зручне, однак інструкції могли б бути ще трохи детальнішими.

💡 **Побажання:**  
Було б цікаво побачити приклади складніших сценаріїв використання Pipenv або Poetry з кількома залежностями.
