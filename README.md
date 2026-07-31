# OWASP-Webgoat

## Мета: Знайомство з A01:2025 Broken Access Control

#### Середовище: Kali Linux, Docker engine, OWASP WebGoat container.
Для кращого розуміння потрібно пройти попередні кроки з мануала WebGoat. У меню оберімо розділ (А1) Broken Access Control та підрозділ Hijack session.

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

<img width="1615" height="415" alt="image" src="https://github.com/user-attachments/assets/d8c32f74-a5cc-4b0b-b371-820a7a6220e1" />

<img width="1438" height="812" alt="image" src="https://github.com/user-attachments/assets/52c1e39c-c241-4126-a4a7-88cd30f2e1fb" />

<img width="1588" height="890" alt="image" src="https://github.com/user-attachments/assets/94979d23-d8d3-411e-8788-cc548ac2d9be" />

























