# <p align="center">Rounded Tk</p>

Rounded Tk is a Python library that allows you to easily create rounded windows and widgets with Python Tkinter.

## 🧐 Features    
- Modern and beautiful rounded widgets
- Easiest way to implement hover actions

## 🛠️ Install
To use it, you need to copy the `RoundedTk.py` file into your project. Then, add the following import statement in your Python code:

```python
from RoundedTk import *
```


## 🧑🏻‍💻 Usage

This library works with Tkinter and other user-interface libraries, such as [ttkbootstrap](https://github.com/israel-dryer/ttkbootstrap). I rrecommend using ttkbootstrap, and in my examples, I will use it.




Create a rounded Window (Windows Only):


```python
from RoundedTk import *
import ttkbootstrap as ttk

root = RoundedWindow(ttk.Window(), percent=10)


root.mainloop()
```


In fact, RoundedWindow is just a tk.Canvas widget, sso it doesn't have properties like ```root.title()``` or others, However, you can use  ```root.root.title()```.


the same example but with tkinter:

```python
from RoundedTk import *
import tkinter as tk

root = RoundedWindow(tk.Tk(), percent=10)


root.mainloop()
```
        
