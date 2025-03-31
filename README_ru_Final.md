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
