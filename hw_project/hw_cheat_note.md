коротка "шпаргалка" по виконанню ДЗ
послідовність виконання ДЗ у відповідності до конспекту

1. Створюємо проєкт на Джанго:
    1.1 У консолі команда: django-admin startproject quotes_toscrape
2. Створюємо БД в Докері для проєкту на Джанго:
    2.1 У консолі команда: docker run --name hwapp-postgres -p 5432:5432 -e POSTGRES_PASSWORD=123456 -d postgres
3. Змінюємо у файлі quotes_toscrape/settings.py посилання на БД:
            DATABASES = {
                'default': {
                    'ENGINE': 'django.db.backends.postgresql_psycopg2',
                    'NAME': 'postgres',
                    'USER': 'postgres',
                    'PASSWORD': '123456',
                    'HOST': '127.0.0.1',
                    'PORT': '5432',
                }
            }
4. Застосовуємо початкову міграцію:
    4.1 У консолі команда: python manage.py migrate
5. Створюємо суперкористувача:
    5.1 У консолі команда: python manage.py createsuperuser / Далі у консолі вводимо дані відповідно до наступного шаблону:
        Username (leave blank to use 'hewlettpackard'): admin
        Email address: admin@i.ua
        Password: 1111
        Password (again): 1111
        Bypass password validation and create user anyway? [y/N]: y
6. Запускаємо сервер розробки для тестової перевірки роботи застосунку:
    6.1 У консолі команда: python manage.py runserver
    при успішному запуску отримаємо за посиланням http://127.0.0.1:8000/ веб сторінку із наступним змістом The install worked successfully! Congratulations!
7. У Django для розмежування різних компонентів цілого проекту створюються окремі застосунки. Основний наш застосунок буде:
    7.1 У консолі команда: python manage.py startapp quotesapp
8. Тепер необхідно в settings.py додати застосунок quotesapp в константу INSTALLED_APPS.
9. Створюємо моделі у файлі quotesapp/models.py
10. Виконуємо міграцію для врахування створених моделей:
    10.1 У консолі команда: python manage.py makemigrations
11. Створюємо таблиці у БД:
    11.1 У консолі команда: python manage.py migrate
12. Виконуємо реєстрацію моделей у застосунку у файлі quotesapp/admin.py
13. Додаємо головну сторінку застосунку - створюємо шаблон index.html в папці quotesapp/templates/quotesapp. Для початку у файл index.html запишемо код із конспекту (в подальших пунктах цей файл зміниться відповідно до вимог ДЗ)
14. Всередині файлу quotesapp/views.py створюємо функцію main для обробки запитів до застосунку. Для початку запишемо код із конспекту (в подальших пунктах цей файл зміниться відповідно до вимог ДЗ)
15. Додаємо маршрутизацію всередину файлу проекту quotes_toscrape/urls.py. Для початку запишемо код із конспекту (в подальших пунктах цей файл зміниться відповідно до вимог ДЗ) (р.22)
16. Створюємо файл quotesapp/urls.py та додаємо маршрут. Для початку запишемо код із конспекту (в подальших пунктах цей файл зміниться відповідно до вимог ДЗ)
17. Cтворюємо базовий шаблон base.html (quotes_toscrape/quotesapp/templates/quotesapp/base.html), від якого будемо наслідувати інші шаблони. Шаблон коду із конспекту.
18. Всередині файлу налаштувань quotes_toscrape/quotes_toscrape/settings.py у змінній STATIC_URL  визначаємо, де зберігатимуться статичні ресурси: STATIC_URL = "static/"
19. Створюємо файл style.css на шляху quotes_toscrape/quotesapp/static/quotesapp/style.css. Шаблон коду із конспекту.
20. Cтворюємо  шаблон tag.html (quotes_toscrape/quotesapp/templates/quotesapp/tag.html). Шаблон коду із конспекту.
21. Cтворюємо форми form, які відповідатимуть за коректність введених даних та зберігатимуть результат введення в БД (quotes_toscrape/quotesapp/forms.py)
22. У файлі quotes_toscrape/quotesapp/views.py додати функцію обробник tag, яка відображатиме шаблон tag.html та оброблятиме POST запити на створення нових тегів
23. Додаємо всередину файлу quotes_toscrape/quotesapp/urls.py маршрут з обробником тегів
24. Для відомраження тегів на головній сторінці index.html необхідно зробити  механізм створення власних тегів для шаблонів:
24.1  За шляхом quotes_toscrape/quotesapp/templatetags/extract_tags.py створюємо файл extract_tags.py. Код із конспекту.
24.2 у шаблоні головної сторінки (index.html) на початку необхідно підвантажити попередній файл таким кодом - {% load extract_tags %} 

Додавання авторів

24. Cтворюємо  шаблон author.html (quotes_toscrape/quotesapp/templates/quotesapp/author.html). Шаблон коду із конспекту та допрацьовуємо відповідно до даних які є в монго ДБ (fullname, born_date, born_location bio).
25. Cтворюємо форми form, які відповідатимуть за коректність введених даних та зберігатимуть результат введення в БД (quotes_toscrape/quotesapp/forms.py)
26. У файлі quotes_toscrape/quotesapp/views.py додати функцію обробник author, яка відображатиме шаблон author.html та оброблятиме POST запити на створення нових авторів
27. Додаємо всередину файлу quotes_toscrape/quotesapp/urls.py маршрут з обробником авторів

Додавання цитат

28. Cтворюємо шаблон для додавання цитати (quotes_toscrape/quotesapp/templates/quotesapp/quote.html). Основа з конспекту, всередині змінене поле для вибору автора (аналогічно вибору тега).
29. Створюємо форму для цитат всередині файлу quotes_toscrape/quotesapp/forms.py
30. Додамо функцію представлення цитати у файл quotes_toscrape/quotesapp/views.py. Основа з конспекту

Сторінка відображення цитати

31. Додамо функцію detail для виведення шаблону цитати у файл quotes_toscrape/quotesapp/views.py Основа з конспекту але дописуємо відображення автора.
32. Додаємо всередину файлу quotes_toscrape/quotesapp/urls.py маршрут з відображення вмісту цитати. Шаблон коду із конспекту
33. Cтворюємо  шаблон detail.html (quotes_toscrape/quotesapp/templates/quotesapp/detail.html). Шаблон коду із конспекту та допрацьовуємо відповідно до вимог ДЗ

Відображення списку цитат

34. Оновимо функцію main у файлі quotes_toscrape/quotesapp/views.py (Шаблон коду із конспекту із змінними відповідно до ДЗ)
35. Оновимо головну сторінку index.html для відображення усіх нотаток (Основа із конспекту а далі наскільки фантазії вистачить)




Сторінка авторів
1. Додамо функцію about_author для виведення сторінки автора у файлі quotes_toscrape/quotesapp/views.py (Аналогічно цитатам).
2. Додаємо всередину файлу quotes_toscrape/quotesapp/urls.py маршрут до сторінки автора. Шаблон коду із конспекту
3. Cтворюємо  шаблон about_author.html (quotes_toscrape/quotesapp/templates/quotesapp/about_author.html). (аналогічно до сторінки відображення цитати)


Додавання користувачів

1. Створюємо новий застосунок users (команда в терміналі python manage.py startapp users)
2. Тепер необхідно в settings.py додати наш застосунок users у константу INSTALLED_APPS
3. У модулі quotes_toscrape/urls.py додамо маршрут на наш новий застосунок users ('path('users/', include('users.urls')),')
4. Створимо файл forms.py всередині застосунку users (quotes_toscrape/users/forms.py) Код з конспекту
5. Створимо у файлі  quotes_toscrape/users/views.py обробник маршруту signupuser. Код з конспекту
6. Створимо шаблон signup.html в папці quotes_toscrape/users/templates/users. Код з конспекту, змінюємо лише назву основного застосунку
7. Створюємо файл urls.py всередині застосунку users (quotes_toscrape/users/urls.py) і поміщаємо туди маршрут реєстрації користувача. Код з конспекту

Аутентифікація

1. У файлі forms.py  (quotes_toscrape/users/forms.py) додаємо форму RegisterForm та LoginForm. Код з конспекту
2. Створимо шаблон login.html в папці quotes_toscrape/users/templates/users. Код з конспекту, змінюємо лише назву основного застосунку
3. Створимо у файлі  quotes_toscrape/users/views.py обробник маршруту loginuser. Код з конспекту 
4. Додаємо маршрут для входу користувачів у файл quotes_toscrape/users/urls.py. Код з конспекту 

Вихід користувача

1. Створимо у файлі  quotes_toscrape/users/views.py обробник маршруту logout. Код з конспекту 
2. Додаємо маршрут для виходу користувачів у файл quotes_toscrape/users/urls.py. Код з конспекту

Змінюємо головну сторінку

1. У меню навігації у шаблоні головної сторінки index.html додамо перевірку аутентифікації. Код з конспекту


Код для завантаження даних з MongoDB в Postgres
із додаткового відео курсу

DONE !!!
мінімальні вимоги до проєкту працюють.



