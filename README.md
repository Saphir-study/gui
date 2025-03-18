# GUI: Tkinter
### Перед началом работы
1. Убедитесь, что у вас установлен Python 3.x. Мы будем использовать одну из базовых библиотек, потому установка дополнительного ПО не потребуется. 
2. Скачайте ZIP с этого гитхаба
3. Попытайтесь запустить код. Если при запуске кода происходят ошибки, пролистните этот README до конца, скопируйте код, вставьте его в новый пустой документ и сохраните его как код для Python. 
4. Если проблема не решена, скажите об этом кому-нибудь из моей команды. 

Я буду рассказывать об библиотеке Tkinter. На каждом этапе вы будете встречать как просто примеры для наглядности, так и примеры их моего кода.  


# Что такое Tkinter?

**Tkinter** — это стандартная библиотека Python для создания графических пользовательских интерфейсов (GUI). Она позволяет создавать окна, кнопки, текстовые поля и другие элементы интерфейса. Tkinter основан на библиотеке Tk, которая изначально была разработана для языка Tcl.

## Основные принципы работы Tkinter

### 1. Главное окно
Каждое приложение на Tkinter начинается с создания главного окна. Это окно является контейнером для всех остальных элементов интерфейса. Создается оно с помощью класса `Tk`:


#### Пример:
```python
import tkinter as tk

root = tk.Tk()
root.title("Мое приложение")
root.mainloop()
```

#### Пример из моего кода:
```python
root = tk.Tk()
root.title("Calculator")
root.geometry("300x400")
```




### 2. Виджеты

**Виджеты** — это элементы интерфейса, такие как кнопки, метки, текстовые поля и т.д. В Tkinter каждый виджет является объектом определенного класса. Например:

- **`tk.Label`** — метка для отображения текста.
- **`tk.Button`** — кнопка, которая выполняет действие при нажатии.
- **`tk.Entry`** — поле для ввода текста.
- **`tk.Frame`** — контейнер для группировки других виджетов.



#### Пример создания кнопки:
```python
button = tk.Button(root, text="Нажми меня", command=some_function)
button.pack()
```


#### Примеры из моего кода:

**`tk.Entry`** — поле для ввода текста.
```python
input_field = tk.Entry(input_frame, font=('arial', 18, 'bold'), textvariable=input_text, width=50, bg="#eee", bd=0, justify=tk.RIGHT)
```

**`tk.Button`** — кнопки калькулятора
```python
tk.Button(buttons_frame, text=button, fg="black", width=10, height=3, bd=0, bg="#fff", cursor="hand2",
          command=lambda x=button: button_click(x) if x != '=' else button_equal())
```

**`tk.Frame`** — контейнер для группировки виджетов.
```python
input_frame = tk.Frame(root, width=312, height=50, bd=0, highlightbackground="black", highlightcolor="black", highlightthickness=1)
buttons_frame = tk.Frame(root, width=312, height=272.5, bg="grey")
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

Пример обработки нажатия кнопки:
```python
def on_button_click():
    print("Кнопка нажата!")

button = tk.Button(root, text="Нажми меня", command=on_button_click)
button.pack()
```
### 5. Переменные Tkinter

Tkinter предоставляет специальные переменные ( **`StringVar`**,  **`IntVar`**,  **`DoubleVar`** и т.д.), которые позволяют связывать данные с виджетами. Например,  **`StringVar`** используется для хранения текста, который может быть связан с меткой или полем ввода.

Пример использования  **`StringVar`**:
```python
text_var = tk.StringVar()
label = tk.Label(root, textvariable=text_var)
text_var.set("Привет, Tkinter!")
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
