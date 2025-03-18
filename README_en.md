# GUI: Tkinter

### Before You Start
1. Make sure you have Python 3.x installed. We will use one of the built-in libraries, so no additional software installation is required.
2. Download the ZIP from this GitHub.
3. Try running the code. If you encounter errors copy the code, paste it into a new empty document, and save it as a Python file.
4. If the problem is not resolved, let someone from my team know.

I will be talking about the Tkinter library. At each stage, you will first see a simple example for clarity, followed by how it is used in my code.

# What is Tkinter?

**Tkinter** is the standard Python library for creating graphical user interfaces (GUI). It allows you to create windows, buttons, text fields, and other UI elements. Tkinter is based on the Tk library, which was originally developed for the Tcl language.

## Basic Principles of Tkinter

### 1. Main Window
Every Tkinter application starts by creating a main window. This window serves as a container for all other UI elements. It is created using the `Tk` class:

#### Example:
```python
import tkinter as tk

root = tk.Tk()
root.title("My Application")
root.mainloop()
```

#### Example from my code:
```python
root = tk.Tk()
root.title("Calculator")
root.geometry("300x400")
```




### 2. Widgets

**Widgets** — are UI elements such as buttons, labels, text fields, etc. In Tkinter, each widget is an instance of a specific class. For example:

- **`tk.Label`** — a label for displaying text.
- **`tk.Button`** — a button that performs an action when clicked.
- **`tk.Entry`** — a text input field.
- **`tk.Frame`** — a container for grouping other widgets.



#### Example of creating a button:
```python
button = tk.Button(root, text="Click me", command=some_function)
button.pack()
```


#### Examples from my code:

**`tk.Entry`** — text input field:
```python
input_field = tk.Entry(input_frame, font=('arial', 18, 'bold'), textvariable=input_text, width=50, bg="#eee", bd=0, justify=tk.RIGHT)
```

**`tk.Button`** — calculator buttons:
```python
tk.Button(buttons_frame, text=button, fg="black", width=10, height=3, bd=0, bg="#fff", cursor="hand2",
          command=lambda x=button: button_click(x) if x != '=' else button_equal())
```

**`tk.Frame`** — container for grouping widgets:
```python
input_frame = tk.Frame(root, width=312, height=50, bd=0, highlightbackground="black", highlightcolor="black", highlightthickness=1)
buttons_frame = tk.Frame(root, width=312, height=272.5, bg="grey")
```




### 3. Geometry Management

To display widgets in the window, you need to place them using one of three geometry managers:

- **`pack()`** — automatically arranges widgets in the window.
- **`grid()`** — arranges widgets in a table format (rows and columns).
- **`place()`** — allows specifying exact coordinates for widget placement.

#### Example using **`grid()`**:

```python
label = tk.Label(root, text="Hello, Tkinter!")
label.grid(row=0, column=0)
```


#### Example from my code

**`pack()`** — placing widgets:
```python
input_frame.pack(side=tk.TOP)
buttons_frame.pack()
```

**`grid()`** — arranging buttons in a table format:
```python
tk.Button(buttons_frame, text=button, ...).grid(row=row, column=col, padx=1, pady=1)
```



### 4. Event Handling

Tkinter allows reacting to user actions, such as **button clicks** or **text input**. This is done using the `command` parameter in widgets (e.g., buttons) or event binding with the `bind` method.

#### Example of handling a button click:
```python
def on_button_click():
    print("Button clicked!")

button = tk.Button(root, text="Click me", command=on_button_click)
button.pack()
```

#### Example from my code

**`button_click`**  — handling button clicks:
```python
def button_click(item):
    global expression
    expression = expression + str(item)
    input_text.set(expression)
```

**`button_clear`** — clearing the input field:
```python
def button_clear():
    global expression
    expression = ""
    input_text.set("")
```

**`button_equal`** — calculating the result:
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


### 5. Tkinter Variables

Tkinter provides special variables ( **`StringVar`**,  **`IntVar`**,  **`DoubleVar`** etc.) that allow linking data to widgets. For example, **`StringVar`** is used to store text that can be linked to a label or input field.

```python
text_var = tk.StringVar()
label = tk.Label(root, textvariable=text_var)
text_var.set("Hello, Tkinter!")
```

#### Example from my code
**`tk.StringVar`** — linking text to an input field:
```python
input_text = tk.StringVar()
input_field = tk.Entry(..., textvariable=input_text)
```
