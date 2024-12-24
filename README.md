# genpass
import tkinter as tk  # Импортируем модуль tkinter для создания GUI
import random         # Импортируем модуль random для генерации случайных чисел
import string         # Импортируем модуль string для доступа к стандартным наборам символов

def generate_password(length, use_lowercase, use_digits, use_special):
    characters = ""  # Инициализируем пустую строку для набора символов

    if use_lowercase:  # Если выбрано использование строчных букв
        characters += string.ascii_lowercase  # Добавляем строчные буквы [a-z]
    if use_digits:  # Если выбрано использование цифр
        characters += string.digits  # Добавляем цифры [0-9]
    if use_special:  # Если выбрано использование специальных символов
        characters += "!@#$%"  # Добавляем специальные символы (!, @, #, $, %)

    if characters:  # Если набор символов не пустой
        return ''.join(random.choice(characters) for _ in range(length))  # Генерируем случайную строку заданной длины
    else:  # Если ни один тип символов не выбран
        return "Выберите хотя бы один тип символов"  # Возвращаем сообщение об ошибке

def on_generate():  # Функция-обработчик нажатия кнопки "Сгенерировать пароль"
    length = int(length_entry.get())  # Получаем длину пароля из текстового поля
    use_lowercase = lowercase_var.get()  # Получаем состояние флажка "строчные буквы"
    use_digits = digits_var.get()  # Получаем состояние флажка "цифры"
    use_special = special_var.get()  # Получаем состояние флажка "специальные символы"

    password = generate_password(length, use_lowercase, use_digits, use_special)  # Генерация пароля
    password_var.set(password)  # Устанавливаем сгенерированный пароль в виджет Entry

# Создание основного окна
root = tk.Tk()  # Создаем главное окно приложения
root.title("Генератор паролей")  # Задаем заголовок окна

# Переменные для хранения состояний чекбоксов
lowercase_var = tk.BooleanVar()  # Переменная для состояния флажка "строчные буквы"
digits_var = tk.BooleanVar()  # Переменная для состояния флажка "цифры"
special_var = tk.BooleanVar()  # Переменная для состояния флажка "специальные символы"

# Виджеты интерфейса
length_label = tk.Label(root, text="Длина пароля:")  # Метка для обозначения поля ввода длины пароля
length_label.pack()  # Размещаем метку в окне

length_entry = tk.Entry(root)  # Поле ввода для указания длины пароля
length_entry.pack()  # Размещаем поле ввода в окне
length_entry.insert(0, "12")  # Устанавливаем начальное значение длины пароля равным 12

lowercase_checkbox = tk.Checkbutton(root, text="Включить алфавит нижнего регистра [a-z]",
                                    variable=lowercase_var)  # Флажок для выбора строчных букв
lowercase_checkbox.pack()  # Размещаем флажок в окне

digits_checkbox = tk.Checkbutton(root, text="Включить цифры [0-9]",
                                 variable=digits_var)  # Флажок для выбора цифр
digits_checkbox.pack()  # Размещаем флажок в окне

special_checkbox = tk.Checkbutton(root, text="Включить спецсимволы [! @ # $ %]",
                                  variable=special_var)  # Флажок для выбора специальных символов
special_checkbox.pack()  # Размещаем флажок в окне

generate_button = tk.Button(root, text="Сгенерировать пароль",
                            command=on_generate)  # Кнопка для запуска генерации пароля
generate_button.pack()  # Размещаем кнопку в окне

password_label = tk.Label(root, text="Сгенерированный пароль:")  # Метка для обозначения поля вывода пароля
password_label.pack()  # Размещаем метку в окне

password_var = tk.StringVar()  # Переменная для хранения сгенерированного пароля
password_display = tk.Entry(root, textvariable=password_var,
                            state='readonly', width=30)  # Поле для отображения сгенерированного пароля
password_display.pack()  # Размещаем поле в окне

# Запуск основного цикла
root.mainloop()  # Запускаем главный цикл приложения
