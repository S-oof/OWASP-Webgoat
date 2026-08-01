# OWASP-Webgoat

## Мета: Знайомство з A01:2025 Broken Access Control

#### Середовище: Kali Linux, Docker engine, OWASP WebGoat container.
Для кращого розуміння потрібно пройти попередні кроки з мануала WebGoat. У меню оберімо розділ (А1) Broken Access Control.

## Hijack a session

### Концепція
Розробники прикладного програмного забезпечення, які створюють власні ідентифікатори сесій (session IDs), часто забувають забезпечити рівень складності та рандомізації, необхідний для безпеки. Якщо специфічний ідентифікатор сесії користувача не є складним і випадковим, додаток стає надзвичайно вразливим до атак типу «brute force» (перебір) на сесії.

### Цілі
Отримати доступ до автентифікованої сесії, що належить іншому користувачу.

### Основні терміни:
Session ID — ідентифікатор сесії.
Complexity and randomness — складність та випадковість.
Brute force attacks — атаки методом грубої сили (перебору).
Authenticated session — автентифікована сесія (сеанс).

## Хід роботи
Далі переходимо на другу вкладинку (червоний колір означає, що потрібно буде щось зробити і це буде перевірятись).У цьому уроці ми намагаємося передбачити значення «hijack_cookie». Цей використовується для розрізнення автентифікованих та анонімних користувачів WebGoat.

<img width="1441" height="617" alt="image" src="https://github.com/user-attachments/assets/3e23dcf2-8383-407b-a4e8-523ac3cfa744" />

натискаємо "Access", отримуємо помилку та повертаємось до burpsuit, де маємо передивитись вкладинку HTTPhistory:

<img width="1602" height="376" alt="image" src="https://github.com/user-attachments/assets/b3986acf-ad87-4d66-ac49-1c53184bd53e" />

Далі шукаємо відповідь POST, в якої міститься інформація про цю помилку (ключ - це зміст hijack_cookie, яку нам і потрібно "передбачити"):

<img width="1914" height="925" alt="image" src="https://github.com/user-attachments/assets/77479169-5ca3-4dd6-ab4f-461d4591051c" />

Далі натискаємо праву кнопку миші та відправляємо запит до Repeater:

<img width="1903" height="893" alt="image" src="https://github.com/user-attachments/assets/a826be5d-19ba-4fe0-a365-716a5e609f15" />

В Repeater робимо декілька повторів (в цьому прикладі може вистачити 5+ запитів):

<img width="409" height="424" alt="image" src="https://github.com/user-attachments/assets/36049a94-5d45-4133-bbe2-85a30220f297" />

Проаналізуємо як змінюється значення hijack_cookie, копіюємо ці значення в текстовий редактор:

<img width="636" height="514" alt="image" src="https://github.com/user-attachments/assets/4d3c8a97-1eec-4dd2-9b52-b1bc39e63e6a" />

Висновок про логіку створення кукі: перша частина відповідає за сесію користувача, а друга скоріш за все є часовою міткою, або timestamp.
5431752998039514611-1785509151093
5431752998039514612-1785509151646
5431752998039514613-1785509152132
5431752998039514615-1785509152597
5431752998039514616-1785509153038
5431752998039514617-1785509153591
5431752998039514618-1785509154108
5431752998039514619-1785509166521
5431752998039514620-1785509167125
5431752998039514621-1785509167709
5431752998039514622-1785509168348
5431752998039514624-1785509169444
5431752998039514625-1785509170008

Бачимо, що між 5431752998039514613 та 5431752998039514615 може бути сесія 5431752998039514614. Передаємо запит з сесією 5431752998039514613 до intruder:
<img width="1261" height="858" alt="image" src="https://github.com/user-attachments/assets/92cb1cb6-5fc5-44c1-823a-d1ed6ff42b6d" />

В Intruder формуємо свій запит відповідним чином: додаємо hijack_cookie 5431752998039514614-1785509152132, останні дві цифри будемо змінювати, такий собі лайтовий брутфорс
<img width="1273" height="888" alt="image" src="https://github.com/user-attachments/assets/7c813495-5974-417c-83dc-b3a8b3d04d19" />

Натискаємо start attack та чекаємо результатів перебору. У вкладці Response отримуємо "Congratulations! You have successfully completed the assigment."
<img width="1508" height="880" alt="image" src="https://github.com/user-attachments/assets/71e27702-49da-4530-a22f-e14d78152da1" />
А також вкладинка в завданні змінює свій колір з червоного на зелений:
<img width="1822" height="795" alt="image" src="https://github.com/user-attachments/assets/58b2ac1a-e0ed-43d3-9b9a-e225fb834575" />

## Insecure Direct Object References
### Хід роботи
#### 1. АВТЕНТИФІКАЦІЯ
Виконаємо вхід в обліковий запис, використовуючи user tom і password cat.
<img width="808" height="501" alt="image" src="https://github.com/user-attachments/assets/2aca234a-8b44-4bd6-abe2-c9c30b6240e7" />
#### 2. ВІДМІННОСТІ
За допомогою burpsuite знайдемо відмінності, які є у відповіді сервера, проте не відображаються у профілі: 
<img width="1514" height="855" alt="image" src="https://github.com/user-attachments/assets/67b9af8e-b76d-4ec8-8b13-c76a04baa72c" />
У відповідне поле введемо знайдені відмінності:
<img width="1307" height="438" alt="image" src="https://github.com/user-attachments/assets/f0651c4d-1b47-40d9-b9b7-47dde0adffff" />
#### 3. ВГАДУВАННЯ ТА ПЕРЕДБАЧЕННЯ ШАБЛОНІВ
Використаємо userID, знайдений у попередньому пункті, та запишемо Url у відповідне поле:
<img width="1804" height="903" alt="image" src="https://github.com/user-attachments/assets/de8dd8de-87e3-4590-9473-67d85c0bb311" />
#### 4. ГРА З ШАБЛОНАМИ
Аби знайти дані іншого профілю, використаємо Intruder: 
<img width="1919" height="846" alt="image" src="https://github.com/user-attachments/assets/a92269ae-420b-468f-867c-b858614efe51" />
Переглянувши усі токени, знайдемо потрібний із належною інформацією:
<img width="1473" height="842" alt="image" src="https://github.com/user-attachments/assets/10a5a26f-de6b-4b4e-8b2f-1d39378ac411" />
Виконаємо редагування іншого профілю. Для вирішення цього питання потрібно мати актуальний (час обмежений) JSESSIONID. Далі з "свіжого" успішного запиту GET зробити в Repater запит PUT.
<img width="1388" height="726" alt="image" src="https://github.com/user-attachments/assets/007462d2-b20c-43a0-b387-fd3d24aabde3" />
Проаналізувавши  відповідь, усе виконано правильно, проте потрібно ще раз зменшити роль (з 2 до 1). Внесемо відповідні зміни та отримаємо результат:
<img width="1536" height="580" alt="image" src="https://github.com/user-attachments/assets/cd0c1587-3954-466e-b0c6-3eeca11cb01e" />
Як ми можемо побачити, усі вкладинки мають зелений колір. Отже, завдання успішно виконані.
<img width="298" height="263" alt="image" src="https://github.com/user-attachments/assets/bca876e3-e571-41b3-bc7e-77926c819b51" />

## (A3) Injection

### Концепція

Інформація цього модуля призначена для розуміння, що таке Structured Query Language (SQL) і як ним можна маніпулювати для виконання завдань, які не були передбачені розробником.

### Цілі

Користувач отримає базове розуміння того:
-як працює SQL;
-для чого він використовується.

Користувач також отримає базове розуміння:
-що таке SQL-ін’єкція;
-як вона працює.

Користувач продемонструє знання щодо:
-DML, DDL та DCL;
-рядкових SQL-ін’єкцій (String SQL injection);
-числових SQL-ін’єкцій (Numeric SQL injection);
-того, як SQL-ін’єкція порушує тріаду CIA (конфіденційність, цілісність, доступність).

## SQL injection (intro)
### Хід роботи

<img width="970" height="357" alt="image" src="https://github.com/user-attachments/assets/7dbf37d5-12c1-47e3-97d0-500f339770ed" />

<img width="993" height="382" alt="image" src="https://github.com/user-attachments/assets/d5ffe046-f287-4208-be2a-2fc137703826" />

<img width="1018" height="323" alt="image" src="https://github.com/user-attachments/assets/263f22bb-0e73-4e7b-a0d1-a65a33eecb9f" />

<img width="995" height="613" alt="image" src="https://github.com/user-attachments/assets/8d5748ae-b93c-44a9-a1c6-48e260f77fff" />

<img width="1579" height="737" alt="image" src="https://github.com/user-attachments/assets/2d565f5e-78f7-4dc7-8271-f673e6d42ddc" />

<img width="1302" height="797" alt="image" src="https://github.com/user-attachments/assets/a3c03d17-7654-4ec7-a33b-25b9380b4d32" />

<img width="1541" height="605" alt="image" src="https://github.com/user-attachments/assets/3d60d14a-d938-43ca-95b3-e68eeb2df5a4" />

<img width="1658" height="599" alt="image" src="https://github.com/user-attachments/assets/c6277f8d-f958-44b4-846b-2589f426a027" />







