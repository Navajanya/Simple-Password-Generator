from tkinter import *
import random
import string

root = Tk()
root.geometry("400x280") 
root.title("Password Generator")

# Intro text
title = StringVar() 
label = Label(root, textvariable=title).pack() 
title.set("The strength of password:")

def selection():
    # This function can be used to handle selection changes if needed
    pass

choice = IntVar()

R1 = Radiobutton(root, text="POOR", variable=choice, value=1, command=selection).pack(anchor=CENTER)
R2 = Radiobutton(root, text="AVERAGE", variable=choice, value=2, command=selection).pack(anchor=CENTER)
R3 = Radiobutton(root, text="ADVANCED", variable=choice, value=3, command=selection).pack(anchor=CENTER)

labelchoice = Label(root)
labelchoice.pack()

lenlabel = StringVar()
lenlabel.set("Password length:")
lentitle = Label(root, textvariable=lenlabel).pack()

val = IntVar()
spinlength = Spinbox(root, from_=8, to_=24, textvariable=val, width=13).pack()

def callback():
    password = passgen()
    Isum.config(text=password)  # Update the label with the generated password

passgenButton = Button(root, text="Generate password", bd=5, height=2, command=callback, pady=3)
passgenButton.pack()

Isum = Label(root, text="")
Isum.pack(side=BOTTOM)

# Logic for password generation
poor = string.ascii_uppercase + string.ascii_lowercase
average = string.ascii_uppercase + string.ascii_lowercase + string.digits
symbols = """~!@#$%^&*()_-+={}[]:;<>,.?/"""
advance = poor + average + symbols

def passgen():
    length = val.get()
    if choice.get() == 1:
        return "".join(random.choices(poor, k=length))  # Use random.choices for repetition
    elif choice.get() == 2:
        return "".join(random.choices(average, k=length))
    elif choice.get() == 3:
        return "".join(random.choices(advance, k=length))
    else:
        return "Select a strength"

root.mainloop()
