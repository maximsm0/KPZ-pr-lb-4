# Реалізація нової сутності, створення CRUD-операцій та відповідного RESTful API
# Мета
# Закріпити навички створення повноцінної серверної логіки для роботи з новою сутністю за допомогою TypeORM, Express та TypeDI. Ознайомитися з процедурою створення міграцій, перевірки змін у структурі бази даних та тестування REST API через Postman.

# Завдання
# Використовуючи boilerplate-проєкт typeorm-express-typescript, який вже містить реалізацію сутності User та відповідного контролера, необхідно:
Було створено сутність Post з полями:  
- id — унікальний ідентифікатор (UUID, первинний ключ),
- title — обов’язковий рядок,
- content — необов’язковий текст,
- createdAt — дата створення, заповнюється автоматично,
- updatedAt — дата останнього оновлення, оновлюється автоматично.  

Для цієї сутності була створена база даних із відповідною таблицею через TypeORM міграції.  
Реалізовано RESTful API для роботи з постами:  
- Create — створення нового поста,
- Read All — отримання списку всіх постів,
- Read One — отримання одного поста за ID,
- Update — оновлення поста за ID,
- Delete — видалення поста за ID.  

Кожна операція реалізована в окремому контролері з обробкою помилок через кастомний клас CustomError.  
Для маршрутизації створено окремий роутер /posts.  
API протестовано через Postman, підтверджено коректність створення, читання, оновлення та видалення постів.  


# 1. Створити нову сутність Post:
**Визначити поля:**
id: UUID, первинний ключ
title: рядок, обов’язковий
content: текст, необов’язковий
createdAt: дата створення, автоматично заповнюється
updatedAt: дата оновлення, автоматично оновлюється
  
- Створено директорію posts в директорії orm/entities
- Створено файл Post.ts:  
  ![image](https://github.com/user-attachments/assets/71eb3120-ad28-46e2-8afa-23f33a18193c)
# 2. Створити та застосувати міграцію:
1. **Згенерувати міграцію для нової сутності.** 
2. **Запустити міграцію через CLI.**
3. **Перевірити у базі даних (наприклад, через pgAdmin або консоль), що структура таблиці відповідає очікуваній.**

- Введено команду для генерування npm run migration:generate CreatePost
![image](https://github.com/user-attachments/assets/fc64ceec-fb2e-484b-a98c-d3d323a27fad)
- Введено команду для запуску міграції npm run migration:run
![image](https://github.com/user-attachments/assets/25626706-05f5-455e-996c-38b08a5dc05d)
- Нова таблиця posts створена  
![image](https://github.com/user-attachments/assets/eecf1c50-190c-42ba-95e7-6cfd7d52aca7)
# 3. Реалізувати RESTful API для CRUD-операцій:
Create: створення нового поста
Read:
отримання всіх постів
отримання одного поста за ID
Update: оновлення поста за ID
Delete: видалення поста за ID
Використовувати контролер, DTO, роутер та сервіс за прикладом реалізації для User.  
  
- Створюємо каталог для контролерів posts в каталозі controllers:  
![image](https://github.com/user-attachments/assets/fee698c2-8f08-435b-abd7-5e03d227bd4d)
- Створюємо для кожної операції віповідні файли: create.ts, destroy.ts, read.ts, readOne.ts, update.ts та index.ts
![image](https://github.com/user-attachments/assets/1f1d707f-271f-4371-8bee-1a82def9b83a)
- Імплементації операцій:
![image](https://github.com/user-attachments/assets/08cd0666-7b5f-4aa5-9b67-e1fa0da78e7c)
![image](https://github.com/user-attachments/assets/7750824b-1681-462a-99df-ed5baa09d2d7)
![image](https://github.com/user-attachments/assets/5280165a-f179-4a66-ae48-732d40facf2f)
![image](https://github.com/user-attachments/assets/5b388460-d8d4-44e5-abb7-28f83c12d170)

В каталозі routes/v1 створюємо posts.ts:  
![image](https://github.com/user-attachments/assets/e4beb365-058f-4afc-9356-7a36f04c9843)
Та оновлюємо файл index.ts  
![image](https://github.com/user-attachments/assets/99ffeb94-08d5-4454-8531-fa9a955b9cfc)

# 5. Протестувати REST API через Postman:
Створити окрему колекцію для запитів.  
![image](https://github.com/user-attachments/assets/cc84f2c2-00f3-4bbf-a4a3-e7f4bbac746a)
- Перевіряєм створення поста  
![image](https://github.com/user-attachments/assets/362ff312-856f-41aa-b793-9a35693f44ed)
- Перевіряєм отримання всіх постів  
![image](https://github.com/user-attachments/assets/c2cab8fe-8c40-4fd8-97f5-2fdcf073f460)
- Перевіряєм отримання поста за ID  
![image](https://github.com/user-attachments/assets/b42b6a51-6756-447b-90cf-fe4aa2b3f9f9)
- Перевіряєм оновлення поста  
![image](https://github.com/user-attachments/assets/f115ffd2-fa39-46a9-be04-91c179d1f0b8)
після апдейту:
![image](https://github.com/user-attachments/assets/1b90ba41-a389-44f7-9b16-3399d49f3f67)
- Перевіряєм видалення поста
![image](https://github.com/user-attachments/assets/e90c09d6-cec7-4b4e-a185-63a840b6f703)
GET повертає помилку після видалення post
![image](https://github.com/user-attachments/assets/cf986fae-d037-42d6-820e-7faa4be1e3b7)

Структури таблиці у базі даних:  
![image](https://github.com/user-attachments/assets/9db2ef78-45f3-4c17-a626-000e7d0e7835)  
![image](https://github.com/user-attachments/assets/8384d8e3-55ca-428e-b88f-e48000389743)  
![image](https://github.com/user-attachments/assets/6ccac661-c2e3-4877-99d7-4a530a5f5592)  

# Висновок
На цій роботі я навчився створювати нову сутність у базі даних за допомогою TypeORM і генерувати для неї міграції. Реалізував повноцінний REST API для роботи з постами — створення, читання, оновлення та видалення. Перевірив роботу API через Postman, щоб упевнитися, що все працює коректно. Також розібрався, як організувати код у контролерах і маршрутах для зручності підтримки.
