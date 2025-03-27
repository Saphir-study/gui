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

#### Basic Example:
```python
import tkinter as tk

root = tk.Tk()  # Create root window
root.title("My App")  # Window title
root.geometry("400x500")  # Dimensions (width x height)
root.mainloop()  # Main event loop
```

#### Example from my code:
```python
root = tk.Tk()
root.title("Calculator")  # Window title
root.geometry("300x400")  # Fixed window size
```




### 2. Widgets

**Widgets** — are UI elements such as buttons, labels, text fields, etc. In Tkinter, each widget is an instance of a specific class. For example:

- **`tk.Label`** — a label for displaying text.
- **`tk.Button`** — a button that performs an action when clicked.
- **`tk.Entry`** — a text input field.
- **`tk.Frame`** — a container for grouping other widgets.



#### Example of creating a button:
```python
button = tk.Button(
    root,                  # Parent container
    text="Click Me",       # Button text
    command=some_function  # Click handler
)
button.pack()             # Add to window
```


#### Examples from my code:

**`tk.Entry`** — text input field:
```python
input_field = tk.Entry(
    input_frame,                     # Parent frame
    font=('arial', 18, 'bold'),      # Font styling
    textvariable=input_text,         # Linked variable
    width=50,                        # Width in chars
    bg="#eee",                       # Light gray background
    bd=0,                            # No border
    justify=tk.RIGHT                 # Right-aligned text
)
```

**`tk.Button`** — calculator buttons:
```python
tk.Button(
    buttons_frame,                   # Parent container
    text=button,                     # Button label
    fg="black",                      # Text color
    width=10, height=3,              # Dimensions
    bd=0,                            # No border
    bg="#fff",                       # White background
    cursor="hand2",                  # Pointer cursor
    command=lambda x=button:         # Click handler
        button_click(x) if x != '='  # For digits/operators
        else button_equal()          # For equals button
)
```

**`tk.Frame`** — container for grouping widgets:
```python
# Input frame
input_frame = tk.Frame(
    root,                           # Parent window
    width=312, height=50,           # Dimensions
    bd=0,                           # No border
    highlightbackground="black",    # Border color
    highlightcolor="black",         # Active border
    highlightthickness=1            # Border width
)

# Buttons frame
buttons_frame = tk.Frame(
    root,
    width=312, height=272.5,
    bg="grey"                       # Gray background
)
```




### 3. Geometry Management

To display widgets in the window, you need to place them using one of three geometry managers:

- **`pack()`** — automatically arranges widgets in the window.
- **`grid()`** — arranges widgets in a table format (rows and columns).
- **`place()`** — allows specifying exact coordinates for widget placement.

#### Example using **`grid()`**:

```python
label = tk.Label(root, text="Hello Tkinter!")
label.grid(row=0, column=0)  # Place in grid
```


#### Example from my code

**`pack()`** — placing widgets:
```python
input_frame.pack(side=tk.TOP)  # Top section
buttons_frame.pack()            # Below input
```

**`grid()`** — arranging buttons in a table format:
```python
tk.Button(
    buttons_frame,
    text=button,
    # ... other parameters ...
).grid(
    row=row, column=col,  # Grid position
    padx=1, pady=1        # Padding
)
```



### 4. Event Handling

Tkinter allows reacting to user actions, such as **button clicks** or **text input**. This is done using the `command` parameter in widgets (e.g., buttons) or event binding with the `bind` method.

#### Example of handling a button click:
```python
def on_click():
    print("Button clicked!")

button = tk.Button(root, text="Click", command=on_click)
```

#### Example from my code

**`button_click`**  — handling button clicks:
```python
def button_click(item):
    global expression
    current = input_text.get()
    
    # Clear if showing result or digit after number
    if '=' in current or (current and current[-1] not in '+-*/' 
                       and (item.isdigit() or item == '.')):
        expression = ""
        input_text.set("")
    
    # Prevent duplicate decimals
    if item == '.' and '.' in expression.split(' ')[-1]:
        return
    
    expression += str(item)
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
        input_text.set(f"{expression}={result}")  # Show full equation
        expression = result
    except:
        input_text.set("Error")
        expression = ""
```


### 5. Tkinter Variables

Tkinter provides special variables ( **`StringVar`**,  **`IntVar`**,  **`DoubleVar`** etc.) that allow linking data to widgets. For example, **`StringVar`** is used to store text that can be linked to a label or input field.

```python
text_var = tk.StringVar()  # Create variable
label = tk.Label(
    root,
    textvariable=text_var  # Bind to widget
)
text_var.set("New Value")  # Update value
```

#### Example from my code
**`tk.StringVar`** — linking text to an input field:
```python
input_text = tk.StringVar()  # Expression variable
input_field = tk.Entry(
    ...,
    textvariable=input_text  # Bind to entry field
)
```
