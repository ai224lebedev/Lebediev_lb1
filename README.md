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

Файл activity_postcard.xml

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

![image](https://github.com/user-attachments/assets/5d232600-6531-4f49-b589-28b3747375b2)



**Завдання 2**

MainActivity — основна активність, яка запускається першою.

GameEx2 — окрема активність для гри. Ми не робимо її exported=true, бо вона не має intent-filter і не запускається зовнішніми додатками.

Ключові частини коду (GameEx2.kt)

1. Список слів

private val wordsList = listOf("цикл", "мова", "дані", ...)

Слова, з яких випадково вибирається одне для гри.

2. Змінні

private lateinit var currentWord: String
private var score = 0

currentWord — слово, яке треба вгадати.

score — лічильник правильних відповідей.


3. Старт активності

override fun onCreate(savedInstanceState: Bundle?) {
    ...
    startNewRound()
}

При запуску екрана одразу починається перший раунд.


4. startNewRound()

private fun startNewRound() {
    currentWord = wordsList.random()
    var mixed = currentWord.toList().shuffled().joinToString("")
    while (mixed == currentWord) {
        mixed = currentWord.toList().shuffled().joinToString("")
    }
    tvScrambledWord.text = mixed
    etAnswer.setText("")
}

Вибирає нове слово, перемішує його і показує на екрані.


5. btnCheck.setOnClickListener

btnCheck.setOnClickListener {
    val input = etAnswer.text.toString().trim()
    if (input.equals(currentWord, ignoreCase = true)) {
        Toast.makeText(this, "✅ Вірно!", Toast.LENGTH_SHORT).show()
        score++
        tvScore.text = "Рахунок: $score"
        startNewRound()
    } else {
        Toast.makeText(this, "❌ Невірно!", Toast.LENGTH_SHORT).show()
    }
}

Обробляє натискання кнопки. Якщо відповідь правильна:

показує тост "вірно"

додає бал

запускає нове слово

Інакше — повідомляє про помилку.

 Layout (activity_game.xml)
TextView для scrambled слова

EditText — для відповіді

Button — для перевірки

TextView — рахунок

Результат:

![image](https://github.com/user-attachments/assets/8319ac75-2c85-4eb7-a857-4d7e8ad63b8a)

![image](https://github.com/user-attachments/assets/dd912917-9735-466c-805f-639f483a0dc4)

![image](https://github.com/user-attachments/assets/6c3205ed-72d2-4e01-84b8-0e6d1f129808)

![image](https://github.com/user-attachments/assets/91736f46-8aef-4bac-968b-cd3bda337e94)

## **Висновки:**
У процесі виконання лабораторної роботи я:

Ознайомився з основами побудови інтерфейсу користувача (UI) в Android за допомогою XML-розмітки;

Навчився використовувати базові компоненти інтерфейсу: TextView, ImageView, Button, EditText;

Створив простий макет вітальної листівки з фоном, текстом і зображенням;

Реалізував інтерактивну гру Word Scramble, де реалізовано:

випадковий вибір слів;

перемішування букв;

перевірку введеного слова;

підрахунок балів;

Закріпив навички роботи без ViewBinding, використовуючи стандартні методи доступу до елементів через findViewById;

Навчився працювати з кількома активностями, розділяючи логіку листівки та гри.

Отримані знання дозволяють впевнено створювати прості UI-додатки та взаємодіяти з ними через код на Kotlin. Ці навички стануть основою для розробки складніших Android-застосунків.
