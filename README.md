# Lebediev_lb1
# Лабораторна робота 1

# Тема: **Створення макета, взаємодія з елементами UI**

**Мета лабораторної роботи:**

- ознайомитися з принципами побудови інтерфейсу користувача (UI) в Android за допомогою XML-розмітки;
- навчитися створювати макети екранів з використанням основних контейнерів (LinearLayout, ConstraintLayout тощо);
- освоїти підключення та налаштування UI-елементів (`TextView`, `EditText`, `Button`, `ImageView` тощо);
- реалізувати взаємодію користувача з елементами інтерфейсу у коді на Kotlin/Java за допомогою обробників подій (наприклад, `setOnClickListener`);
- сформувати навички роботи з ресурсами (рядки, кольори, розміри) та забезпечити підтримку адаптивності інтерфейсу.

## **Завдання**

### 1. **Розробити вітальну листівку з днем народження.**

Листівка має містити гарний текст, фоновий колір і зображення. Приклад листівки:

![image](https://github.com/user-attachments/assets/3fe91a2b-7eab-4e67-a520-71ddddb2c3cf)


### 2. **Розробити гру Word Scramble.**

Суть гри полягає в наступному:

1. Комп'ютер обирає випадкове слово зі списку слів, перемішує літери в цьому слові і показує гравцеві;
2. Гравець повинен здогадатися - яке слово вибрав комп'ютер і ввести його в поле введення;
3. Якщо гравець вгадав слово - комп’ютер повідомляє гравця, що слово вгадано вірно та гра починається заново;
4. Якщо слово невірне, комп'ютер повідомляє гравця про це і гра триває.


## **Хід роботи**

Завдання 1:
Пояснення коду:
 1) ScrollView
<ScrollView ... >
ScrollView — це контейнер, який дозволяє прокручувати вміст, якщо він не поміщається на екрані.

Використовується, щоб листівка працювала на різних пристроях з різними розмірами екранів.

2) LinearLayout

<LinearLayout ... >
Це контейнер, який розміщує дочірні елементи вертикально (android:orientation="vertical").

android:gravity="center" — вирівнює вміст по центру по горизонталі.

android:padding="16dp" — відступ всередині контейнера.

3) ImageView — кульки

<ImageView
    android:id="@+id/balloonsImage"
    android:layout_width="wrap_content"
    android:layout_height="150dp"
    android:src="@drawable/balloons"
    android:contentDescription="Balloons" />
Відображає зображення кульок (balloons.png) з папки res/drawable.

Висота обмежена 150dp, ширина автоматично підлаштовується.

4) TextView — "Happy Birthday!"

<TextView
    android:id="@+id/happyBirthdayText"
    ...
    android:text="Happy Birthday!" />
Показує привітальний текст.

Великий розмір шрифту (28sp), синій колір, жирний стиль.

5) ImageView — торт

<ImageView
    android:id="@+id/cakeImage"
    android:layout_width="200dp"
    android:layout_height="200dp"
    android:src="@drawable/cake"
    ... />
Відображає зображення торта.

Фіксований розмір 200x200dp.

6) TextView — побажання

<TextView
    android:id="@+id/messageText"
    android:text="Wishing you a beautiful day full of love and happiness"
    ...
/>
Це побажання до дня народження.

Стилізований текст: середній розмір, коричневий колір, вирівнювання по центру.

Відступи додають простору навколо.

7) Button — "Say Thanks"

<Button
    android:id="@+id/showToastButton"
    android:text="Say Thanks"
    ...
/>
Це інтерактивна кнопка, яка, коли користувач натискає, викликає подію в Kotlin-коді.

Наприклад, показує повідомлення "Thank you!" через Toast.

Результат:

![image](https://github.com/user-attachments/assets/24afeac9-b4e1-46b1-9cf4-3aed723f1925)

