# Python-Programming
from tkinter import *
import tkinter.messagebox as tmsg
import os
import time
total=0

def over():
    """if The shopping is over than asking for bill"""
    if (user_name.get()=="" or admin_location == ""):
        """if the important is missed to enter"""
        tmsg.showinfo("Warning","Your admin location or name is empty please enter it")
    else:

        value=tmsg.askquestion("Bill formation",f"Your bill is created and your total is {total} do you want the bill or not?")
        if (value=="yes"):
            if user_location.get()=="":
                tmsg.showinfo("Warning","You had not placed the admin location please place it")
            else:

                path1 = user_location.get()
                path2=admin_location.get()
                tmsg.showinfo("Bill formation",f"Your bill is being created the location is here {path1}")
                with open((f"{path2}\{user_name.get()}.txt"),"a") as f:
                    f.write(f"Total is {total}\nThank You for your shopping\nPlease visit us again\ndate and time is {time.asctime()}")
                with open(f"{path1}\{user_name.get()}.txt","a") as f:
                    with open(f"{path2}\{user_name.get()}.txt","r") as f1:
                        for l in f1.readlines():
                            f.write(l)
                user_entry.set("")
                user_entry_qty.set(0)
                user_name.set("")
                e3.update()
                e1.update()
                e2.update()
        else:
            tmsg.showinfo("Completion","Thank You please visit us again")
            root1.destroy()
            user_entry.set("")
            user_entry_qty.set(0)
            user_name.set("")
            e1.update()
            e2.update()
            e3.update()

m=1
def newi():
   
    """Proceeding furthur after user want to add any new item in the bill"""
    global total
    temp=user_entry_qty.get()
    flag = 0
    for i,j in dict_items.items():
        if i==user_entry.get():
            """if the item entered is there in the list"""
            global m
            """Updating the status bar"""
            l2.insert(END,f"{m}){user_entry.get()}---{user_entry_qty.get()}----Rs{int(user_entry_qty.get())*dict_items[user_entry.get()]}")
            m = m+1
            flag=1
            total =total+int(temp)*j
            total_status.set(f"Total is {total}")
            path2 = admin_location.get()
            with open((f"{path2}\{user_name.get()}.txt"),"a") as f:
                """Appending the information to the admin file"""
                f.write(f">>>>{user_entry.get()}---{temp}\n")

            """Reseting the initial value of the window"""
            user_entry.set("")
            user_entry_qty.set(0)
            e1.update()
            e2.update()
            break
   
    if flag==0:
        """If the item is not found in the list then printing the message box"""
        tmsg.showinfo("No item",f"There is no item like {user_entry.get()}")
        user_entry.set("")
        user_entry_qty.set(0)
        e1.update()
        e2.update()
def addnew():
    l.insert(END,f">>{new_item_label_status.get()}--{new_item_price.get()}")
    dict_items[str(new_item_label_status.get())]=int(new_item_price.get())
    print(dict_items)
    new_item_label_status.set("")
    new_item_entry.update()
    new_item_price.set(0)
    new_item_price_entry.update()


root1 = Tk()
root1.geometry("655x855")
root1.title("Poojan Mart")
# adding introduction statement
Label(root1,text="Welcome To The Poojan Mart\nI Hope You will enjoy my service",font="lucida 20 bold",fg="purple").pack(fill=BOTH)
# taking name and all the locations
user_location = StringVar()
admin_location=StringVar()
f=Frame(root1)
f.pack()
Label(f,text="Enter the location for admin:",font ="lucida 10 bold").pack(side=LEFT,fill=BOTH)
Entry(f,textvariable=admin_location,font ="lucida 10 bold").pack(side=LEFT,ipady=11,fill=BOTH)
f=Frame(root1)
f.pack()
Label(f,text="Enter the location for user:",font="lucida 10 bold").pack(side=LEFT)
Entry(f,textvariable=user_location,font="lucida 10 bold").pack(side=LEFT,ipady=11,pady=4,fill=BOTH)
user_name = StringVar()
f=Frame(root1)
f.pack()
Label(f,text="Enter the name of user:",font="lucida 10 bold").pack(side=LEFT,ipady=11,fill=BOTH)
e3=Entry(f,textvariable=user_name)
e3.pack(side=LEFT)
# makint list box and scroll bar
dict_items = {"bhindi":36,"maggi":10,"potato":25,"onion":45}
scrollbar=Scrollbar()
scrollbar.pack(fill=Y,side=RIGHT)
l=Listbox(root1,yscrollcommand=scrollbar.set)

for i,j in dict_items.items():
    l.insert(END,f">>{i}--{j}")
l.pack()
scrollbar.config(command=l.yview)
# name entry
f=Frame(root1)
f.pack()
user_entry = StringVar()
Label(f,text="Enter the name of item:",font="lucida 10 bold").pack(side=LEFT,fill=BOTH)
e1=Entry(f,textvariable=user_entry,font="lucida 10 bold")
e1.pack(side=LEFT,ipady=11,fill=BOTH)
f=Frame(root1)
f.pack()
user_entry_qty = StringVar()
Label(f,text="Enter the quantity of item:",font="lucida 10 bold").pack(side=LEFT,fill=BOTH)
e2=Entry(f,textvariable=user_entry_qty,font="lucida 10 bold")
e2.pack(side=LEFT,ipady=11,fill=Y)
# printing dynamic total
total_status=StringVar()
f=Frame(root1)
f.pack()
l1=Label(f,text="Hello",textvariable=total_status,font="lucida 10 bold")
l1.pack(side=LEFT,fill=BOTH)
f=Frame(root1)
f.pack()
# making button
Button(f,text="New Item",command=newi,font="lucida 9 bold").pack(side=LEFT,padx=6,fill=BOTH)
Button(f,text="Over",command=over,font="lucida 9 bold").pack(side=LEFT,padx=6,fill=BOTH)
# Making a real time status bar with scroll bar
l2=Listbox(root1,yscrollcommand=scrollbar.set)
l2.pack()
s2=Scrollbar()
s2.pack(fill=Y,side=RIGHT)
s2.config(command=l2.yview)
# for adding new item
f=Frame(root1)
f.pack()
new_item_label_status = StringVar()
Label(f,text="Enter the new item name:",font="lucida 9 bold").pack(side=LEFT,fill=BOTH)
new_item_entry = Entry(f,textvariable=new_item_label_status,font = "lucida 9 bold")
new_item_entry.pack(side=LEFT,pady=16,fill=BOTH)
f=Frame(root1)
f.pack()
new_item_price = IntVar()
Label(f,text="Enter the price of new item:",font="lucida 9 bold").pack(side=LEFT,fill=BOTH)
new_item_price_entry = Entry(f,textvariable=new_item_price,font="lucida 9 bold")
new_item_price_entry.pack(side=LEFT,ipady=16,fill=BOTH)
Button(root1,text="Add the new item",command=addnew,font="lucida 9 bold").pack()
root1.mainloop()
