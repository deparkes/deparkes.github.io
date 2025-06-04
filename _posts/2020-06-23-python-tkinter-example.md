---
layout: post
title: Python Tkinter Example
date: 2020-06-23 17:53:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- example
- GUI
- guide
- python
- tk
- tkinter
- tutorial
- UI
author: deparkes
permalink: "/2020/06/23/python-tkinter-example/"
---
This post works through a simple example of creating a GUI in python using Tkinter. The python tkinter example goes through some simple things that a GUI would need to do such as creating new windows, text input, and labels.
This isn't a tutorial as such, but instead I've tried to pick out a few of the basics of tkinter so that they are in one place. You can use this basic example as a starting point for more sophisiticated GUI applications.
This example is available on <a href="https://github.com/deparkes/tkinter_example">github.</a>

| ![tkinter example]({{site.baseurl}}/assets/2020/06/a_warning_message.png) |
|:--:|
| *tkinter example* |

<h2>Why Tkinter?</h2>
There are a number of <a href="https://wiki.python.org/moin/GuiProgramming">GUI libraries available for python</a>, so why tkinter?
<ul>
<li>
<strong>Portability</strong> - Tkinter is also designed to make use of the existing styling of the operating system it is running in, rather than bringing its own widgets.</li>
<li>
<strong>Simplicity</strong> - Tkinter is also fairly simple to get started with (as you will see in this example), so is good for</li>
<li>
<strong>Availability</strong> - Tkinter is typically packaged with python, so if package availability is a challenge for you, then Tkinter may make sense</li>
</ul>
<h2>An Example</h2>
In this example I'm going to step through the creation of a simple GUI featuring:
<ul>
<li>A main window</li>
<li>Two sub-windows</li>
<li>Creating an alert box</li>
<li>Creating an 'About' menu item</li>
</ul>
I have deliberately left out the less essential parts of the GUI design such as sizing and exact layout. This is important to consider, but for the purposes of learning I find it can distract from the truly essential parts of the code.
<h3>Create The Main Window</h3>
We're going to be making main window that looks like this - two buttons that open sub-windows, and a Help menu.

| ![Main window]({{site.baseurl}}/assets/2020/06/main_window-1.png) |
|:--:|
| *Main window* |

```python
import tkinter
from tkinter import messagebox
import os
window = tkinter.Tk()
window.title("Main Window")
# create a toplevel menu
menubar = tkinter.Menu(window)
helpmenu = tkinter.Menu(menubar)
menubar.add_cascade(label="Help", menu=helpmenu)
helpmenu.add_command(label="About")
# display the menu
window.config(menu=menubar)
btn = tkinter.Button(window, text="Sub-window 1")
btn.pack(anchor='center')
btn2 = tkinter.Button(window, text="Sub-window 2")
btn2.pack(anchor='center')
window.mainloop()
```

At this stage the buttons won't do anything. We'll add that later.
<h3>Add an 'About' box</h3>
Next, we add an 'About' option to the 'Help' menu:

| ![About menu]({{site.baseurl}}/assets/2020/06/about_menu.png) |
|:--:|
| *About menu* |

Clicking that 'About' option will create an 'About box'

| ![About box]({{site.baseurl}}/assets/2020/06/about_box.png) |
|:--:|
| *About box* |

We do this by first creating a function to hold the details of this new 'About' window, along with a corresponding reference to that function in the button click.
First, we'll create a function to hole the 'About' window:

```python
def create_about():
    about_window = tkinter.Toplevel(window)
    about_window.title('About')
    lbl = tkinter.Label(about_window, text="About")
    lbl.config(anchor=tkinter.CENTER)
    lbl.pack(anchor='center')
    btn = tkinter.Button(about_window, text="OK", command=about_window.destroy)
    btn.pack(anchor='center')
```

And then update the 'helpmenu' menu bar to include a command which points to that new function.

```python
helpmenu.add_command(label="About", command=create_about)
```


<h3>Add the First Sub-window</h3>
In this first sub-window, we'll add quite a bit of functionality:
<ul>
<li><strong>Close a window with a click</strong></li>
<li><strong>Add text box / label to a window</strong></li>
<li><strong>Centering text box / label</strong></li>
<li><strong>Get a value from a button click</strong></li>
<li><strong>Use a button to run non-UI functionality</strong></li>
<li><strong>Use a button to create an information box</strong></li>
</ul>
As with the 'about' box, we can keep the details of this new sub-window inside its own function, and then reference this function in the button click.
First we can update the button click to reference a function:

```python
btn = tkinter.Button(window, text="Sub-window 1", command=create_subwindow1)
```

And then add the function itself

```python
def create_subwindow1():
    def retrieve_input():
        entryText = entry.get()
        if os.path.exists(entryText):
            lbl2.config(text='A file')
        else:
            lbl2.config(text='Not a file')
    sub_window = tkinter.Toplevel(window)
    sub_window.title('Sub-window 1')
    lbl = tkinter.Label(sub_window, text="Sub-window 1")
    lbl.config(anchor=tkinter.CENTER)
    lbl.pack(anchor='center')
    btn = tkinter.Button(sub_window, text="Close", command=sub_window.destroy)
    btn.pack(anchor='center')
    lbl2 = tkinter.Label(sub_window, text="")
    lbl2.pack(anchor='center')
    entry = tkinter.Entry(sub_window)
    entry.pack(anchor='center')
    buttonCommit=tkinter.Button(sub_window, text="Check path exists",
                                command=retrieve_input)
    buttonCommit.pack(anchor='center')
    btn2 = tkinter.Button(sub_window, text="Functionality 2", command=lambda: messagebox.showinfo("Info","Not Yet Implemented"))
    btn2.pack(anchor='center')
```

The resulting sub-window should look like this:

| ![Sub-window]({{site.baseurl}}/assets/2020/06/functionality1_file_exists_checker.png) |
|:--:|
| *Sub-window* |

And the 'Not Yet Implemented' info message when we click on Functionality 2 comes up as this:

| ![Not yet implemented info message]({{site.baseurl}}/assets/2020/06/functionality2_not_yet_implemented_window.png) |
|:--:|
| *Not yet implemented info message* |

<h3>Add the Second Sub-window</h3>
Finally we'll add the code for the second sub-window, although this time we are actually going to make a warning window.
<img class="aligncenter size-full wp-image-4777" src="{{site.baseurl}}/assets/2020/06/a_warning_message.png" alt="" width="187" height="153">

| ![Not yet implemented info message]({{site.baseurl}}/assets/2020/06/functionality2_not_yet_implemented_window.png) |
|:--:|
| *Not yet implemented info message* |

Again, we follow the same pattern of updating the button 'command' attribute. A difference here is that rather than creating a separate function, we instead create a inline, <a href="https://realpython.com/python-lambda/">lambda function</a> to hold the message box creation:

```python
btn2 = tkinter.Button(window, text="Sub-window 2", command=lambda: tkinter.messagebox.showwarning("Warning","Warning message"))
```

