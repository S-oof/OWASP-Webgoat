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

<img width="1594" height="433" alt="image" src="https://github.com/user-attachments/assets/f0f4e2f8-ead8-4868-ada4-e7ee89aad4c0" />

<img width="1598" height="887" alt="image" src="https://github.com/user-attachments/assets/8576230f-58bd-45a5-97f0-a94a3819350f" />

<img width="1593" height="882" alt="image" src="https://github.com/user-attachments/assets/ae7d3657-434d-41fd-9adf-1c80932728ad" />

<img width="1596" height="882" alt="image" src="https://github.com/user-attachments/assets/99b6ef41-27f1-469a-a78b-890c64aab9e2" />

<img width="412" height="312" alt="image" src="https://github.com/user-attachments/assets/63a89f9d-f754-4f32-ba51-7ec2889f4da8" />

5431752998039514330-1785498759046
5431752998039514331-1785498762033
5431752998039514333-1785498762437
5431752998039514335-1785498762573
5431752998039514336-1785498762724
5431752998039514337-1785498762871
5431752998039514338-1785498763025
5431752998039514340-1785498763149
5431752998039514341-1785498763275
5431752998039514342-1785498763395

<img width="1565" height="879" alt="image" src="https://github.com/user-attachments/assets/e3e8491f-34f0-46fe-a719-9b11ca4028d4" />








































