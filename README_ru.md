# GUI: Tkinter
### Перед началом работы
1. Убедитесь, что у вас установлен Python 3.x. Мы будем использовать одну из базовых библиотек, потому установка дополнительного ПО не потребуется. 
2. Скачайте ZIP с этого гитхаба
3. Попытайтесь запустить код. Если при запуске кода происходят ошибки, пролистните этот README до конца, скопируйте код, вставьте его в новый пустой документ и сохраните его как код для Python. 
4. Если проблема не решена, скажите об этом кому-нибудь из моей команды. 

Я буду рассказывать об библиотеке Tkinter. На каждом этапе вы будете встречать с начала простой пример примеры для наглядности, а затем как это использовано в моем коде.


# Что такое Tkinter?

**Tkinter** — это стандартная библиотека Python для создания графических пользовательских интерфейсов (GUI). Она позволяет создавать окна, кнопки, текстовые поля и другие элементы интерфейса. Tkinter основан на библиотеке Tk, которая изначально была разработана для языка Tcl.

## Основные принципы работы Tkinter

### 1. Главное окно
Каждое приложение на Tkinter начинается с создания главного окна. Это окно является контейнером для всех остальных элементов интерфейса. Создается оно с помощью класса `Tk`:


#### Пример:
```python
import tkinter as tk

root = tk.Tk()  # Создание корневого окна
root.title("Мое приложение")  # Заголовок
root.geometry("400x500")  # Размеры (ширина x высота)
root.mainloop()  # Главный цикл обработки событий
```

#### Пример из моего кода:
```python
root = tk.Tk()
root.title("Calculator")  # Установка заголовка "Калькулятор"
root.geometry("300x400")  # Фиксированный размер окна
root.resizable(False, False)  # Запрет изменения размера (добавлено в текущей версии)
```




### 2. Виджеты

**Виджеты** — это элементы интерфейса, такие как кнопки, метки, текстовые поля и т.д. В Tkinter каждый виджет является объектом определенного класса. Например:

- **`tk.Label`** — метка для отображения текста.
- **`tk.Button`** — кнопка, которая выполняет действие при нажатии.
- **`tk.Entry`** — поле для ввода текста.
- **`tk.Frame`** — контейнер для группировки других виджетов.



#### Пример создания кнопки:
```python
# Создание простой кнопки
button = tk.Button(
    root,                     # Родительский контейнер
    text="Нажми меня",        # Текст на кнопке
    command=some_function     # Функция-обработчик
)
button.pack()                # Размещение кнопки в окне
```


#### Примеры из моего кода:

**`tk.Entry`** — поле для ввода текста.
```python
input_field = tk.Entry(
    input_frame,                              # Родительский фрейм
    font=('arial', 18, 'bold'),               # Шрифт: Arial 18pt (жирный)
    textvariable=input_text,                  # Привязка к переменной
    width=50,                                 # Ширина в символах
    bg="#eee",                                # Цвет фона (светло-серый)
    bd=0,                                     # Без рамки
    justify=tk.RIGHT                          # Выравнивание текста справа
)
```

**`tk.Button`** — кнопки калькулятора
```python
tk.Button(
    buttons_frame,                            # Контейнер для кнопок
    text=button,                              # Текст с цифрой/оператором
    fg="black",                               # Цвет текста
    width=10,                                 # Ширина кнопки
    height=3,                                 # Высота кнопки
    bd=0,                                     # Без рамки
    bg="#fff",                                # Белый фон
    cursor="hand2",                           # Изменение курсора при наведении
    command=lambda x=button:                  # Обработчик с условием:
        button_click(x) if x != '='           # Для цифр/операторов
        else button_equal()                   # Для кнопки "="
)
```

**`tk.Frame`** — контейнер для группировки виджетов.
```python
# Фрейм для поля ввода
input_frame = tk.Frame(
    root,                                     # Главное окно
    width=312,                                # Ширина в пикселях
    height=50,                                # Высота
    bd=0,                                     # Без рамки
    highlightbackground="black",              # Цвет границы
    highlightcolor="black",                   # Цвет при активации
    highlightthickness=1                      # Толщина границы
)

# Фрейм для кнопок
buttons_frame = tk.Frame(
    root,
    width=312,
    height=272.5,
    bg="grey"                                 # Серый фон
)
```




### 3. Геометрия

Чтобы виджеты отображались в окне, их нужно разместить с помощью одного из трех менеджеров геометрии:

- **`pack()`** — автоматически размещает виджеты в окне.
- **`grid()`** — размещает виджеты в виде таблицы (строках и столбцах).
- **`place()`** — позволяет указать точные координаты для размещения виджета.

#### Пример использования grid():

```python
label = tk.Label(root, text="Привет, Tkinter!")
label.grid(row=0, column=0)
```


#### Пример из моего кода

**`pack()`** — размещение виджетов.
```python
input_frame.pack(side=tk.TOP)
buttons_frame.pack()
```

**`grid()`** — размещение кнопок в виде таблицы.
```python
tk.Button(buttons_frame, text=button, ...).grid(row=row, column=col, padx=1, pady=1)
```



### 4. Обработка событий

Tkinter позволяет реагировать на действия пользователя, такие как нажатие кнопки или ввод текста. Для этого используется параметр **`command`** у виджетов (например, кнопок) или привязка событий с помощью метода **`bind`**.

#### Пример обработки нажатия кнопки:
```python
def on_button_click():
    print("Кнопка нажата!")

button = tk.Button(root, text="Нажми меня", command=on_button_click)
button.pack()
```

#### Пример из моего кода

**`button_click`**  — обработка нажатия кнопок.
```python
def button_click(item):
    global expression
    expression = expression + str(item)
    input_text.set(expression)
```

**`button_clear`** — очистка поля ввода.
```python
def button_clear():
    global expression
    expression = ""
    input_text.set("")
```

**`button_equal`** — вычисление результата.
```python
def button_equal():
    global expression
    try:
        result = str(eval(expression))
        input_text.set(result)
        expression = result
    except:
        input_text.set("Error")
        expression = ""
```


### 5. Переменные Tkinter

Tkinter предоставляет специальные переменные ( **`StringVar`**,  **`IntVar`**,  **`DoubleVar`** и т.д.), которые позволяют связывать данные с виджетами. Например,  **`StringVar`** используется для хранения текста, который может быть связан с меткой или полем ввода.

#### Пример использования  **`StringVar`**:
```python
text_var = tk.StringVar()
label = tk.Label(root, textvariable=text_var)
text_var.set("Привет, Tkinter!")
```

#### Пример из моего кода
**`tk.StringVar`** — связь текста с полем ввода.
```python
input_text = tk.StringVar()
input_field = tk.Entry(..., textvariable=input_text)
```



## Пример: Калькулятор на Tkinter
В качестве примера использования Tkinter рассмотрим простой калькулятор, который выполняет базовые арифметические операции.

Код калькулятора

```python
import tkinter as tk

# Функции для обработки нажатий кнопок
def button_click(item):
    global expression
    expression += str(item)
    input_text.set(expression)

def button_clear():
    global expression
    expression = ""
    input_text.set("")

def button_equal():
    global expression
    try:
        result = str(eval(expression))
        input_text.set(result)
        expression = result
    except:
        input_text.set("Ошибка")
        expression = ""

# Создание главного окна
root = tk.Tk()
root.title("Калькулятор")
root.geometry("300x400")

expression = ""
input_text = tk.StringVar()

# Поле для ввода
input_field = tk.Entry(root, textvariable=input_text, font=('arial', 18), bd=10, justify=tk.RIGHT)
input_field.pack(fill=tk.BOTH, ipadx=8, pady=10, padx=10)

# Кнопки
buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    '0', '.', '=', '+'
]

frame = tk.Frame(root)
frame.pack()

row, col = 0, 0
for button in buttons:
    tk.Button(frame, text=button, width=5, height=2, command=lambda x=button: button_click(x) if x != '=' else button_equal()).grid(row=row, column=col)
    col += 1
    if col > 3:
        col = 0
        row += 1

# Кнопка очистки
tk.Button(root, text="C", width=20, height=2, command=button_clear).pack()

# Запуск приложения
root.mainloop()
```

### Основные элементы приложения

- **Главное окно**: Создается с помощью `tk.Tk()`.
- **Поле ввода**: Используется `tk.Entry` для отображения вводимых данных и результатов.
- **Кнопки**: Создаются с помощью `tk.Button` и привязаны к функциям, которые обрабатывают нажатия.
- **Обработка событий**: Функции `button_click`, `button_clear` и `button_equal` реагируют на действия пользователя.



```python

```
