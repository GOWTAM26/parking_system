# parking_system
#import modules
 
from tkinter import *
from PIL import ImageTk,Image
from tkinter import messagebox  
import os
 
# Designing window for registration
 
def register():
    global register_screen
    register_screen = Toplevel(main_screen)
    register_screen.title("Register")
    register_screen.geometry("650x480")
    global username
    global password
    global username_entry
    global password_entry
    username = StringVar()
    password = StringVar()
    Label(register_screen, text="Please enter details below",fg="steel blue",font=( 'Bradley Hand ITC' ,20, 'bold' )).place(x=200,y=0)
    username_lable = Label(register_screen, text="Username",font=( 'Bradley Hand ITC' ,17, 'bold' ),)
    username_lable.place(x=300,y=50)
    username_entry = Entry(register_screen, font=( 20 ),bd=2,textvariable=username)
    username_entry.place(x=300,y=100)
    password_lable = Label(register_screen, text="Password",font=( 'Bradley Hand ITC' ,17, 'bold' ))
    password_lable.place(x=300,y=150)
    password_entry = Entry(register_screen,font=( 20),bd=2, textvariable=password, show='*')
    password_entry.place(x=300,y=200)
    Label(register_screen, text="").place(x=300,y=250)
    Button(register_screen, text="Register", width=10, height=1, bg='brown',fg='white', command = register_user).place(x=300,y=300)
 
 
# Designing window for login 
 
def login():
    global login_screen
    login_screen = Toplevel(main_screen)
    login_screen.title("Login")
    login_screen.geometry("650x480")
    Label(login_screen, text="Please enter details below to login",font=( 'Bradley Hand ITC' ,17, 'bold' )).place(x=130,y=0)
    global username_verify
    global password_verify
 
    username_verify = StringVar()
    password_verify = StringVar()
 
    global username_login_entry
    global password_login_entry
 
    Label(login_screen,font=( 'Bradley Hand ITC' ,17,'bold' ), text="Username").place(x=250,y=50)
    username_login_entry = Entry(login_screen,font=(17) ,textvariable=username_verify)
    username_login_entry.place(x=250,y=100)
    Label(login_screen,font=( 'Bradley Hand ITC' ,17, 'bold' ), text="Password").place(x=250,y=150)
    password_login_entry = Entry(login_screen,font=(17 ), textvariable=password_verify, show= '*')
    password_login_entry.place(x=250,y=200)
    Button(login_screen, text="Login", width=10, height=1,bg='brown',fg='white', command = login_verify).place(x=275,y=250)
 # Implementing event on register button
 
def register_user():
 
    username_info = username.get()
    password_info = password.get()
 
    file = open(username_info, "w")
    file.write(username_info + "\n")
    file.write(password_info)
    file.close()
 
    username_entry.delete(0, END)
    password_entry.delete(0, END)
 
    messagebox.showinfo("Registration","Registration Success")
 # Implementing event on login button 
 
def login_verify():
    username1 = username_verify.get()
    password1 = password_verify.get()
    username_login_entry.delete(0, END)
    password_login_entry.delete(0, END)
 
    list_of_files = os.listdir()
    if username1 in list_of_files:
        file1 = open(username1, "r")
        verify = file1.read().splitlines()
        if password1 in verify:
            login_sucess()
 
        else:
            password_not_recognised()
 
    else:
        user_not_found()
 # Designing popup for login success
#=========================================================================================================================================================
def login_sucess():     
    messagebox.showinfo("Login","Login Sucess") 
    def datasave():
        f=open("REPORT.txt","a")
        f.write("\n\n\n------------------------------------------------------------------------------------------------------------------------------------\n")
        f.write("**************--------D E T A I L S--------*************\n")
        f.write("------------------------------------------------------------------------------------------------------------------------------------\n")
        f.write("Name-->")
        f.write(name.get())
        f.write("\n Phone : %d \n" %phone.get())
        f.write("\n Registration Id : %d \n" %registrationid.get())
        if var.get()==1 :
            f.write("Gender-->Male\n")
        else:
            f.write("Gender-->Female\n")
        f.write("\n Email-->")
        f.write(email.get())    
        """
        f.write("State-->")
        f.write(c.get())
        f.write("\nProgram selected-->")
        ch=0
        if var1.get()==1 :
                f.write("   Subsidise")
        if var2.get()==1 :
                f.write("   Normal")
        f.write("\n Address-->")
        f.write(address.get())
        """
    
        f.close()
        messagebox.showinfo("Succesful","Data Submitted Succesfully")
        delete_login_success()
        
    
    global login_success_screen
    login_success_screen = Toplevel(login_screen)
    login_success_screen.title("Success")
    login_success_screen.geometry("850x600")
    login_success_screen.title("Registration Form")

    label_0 = Label(login_success_screen, text="Registration form",width=30,font=("bold", 20),fg='steel blue')
    label_0.place(x=250,y=53)

    name = StringVar()
    phone = IntVar()
    registrationid = IntVar()
    label_1 = Label(login_success_screen, text="FullName",width=20,font=("bold", 10))
    label_1.place(x=250,y=130)

    entry_1 = Entry(login_success_screen,textvariable=name)
    entry_1.place(x=440,y=130)

    label_2 = Label(login_success_screen, text="Phone no",width=20,font=("bold", 10))
    label_2.place(x=250,y=180)

    entry_2 = Entry(login_success_screen,textvariable=phone)
    entry_2.place(x=440,y=180)
    
    label_3 = Label(login_success_screen, text="Registration Id",width=20,font=("bold", 10))
    label_3.place(x=250,y=230)

    entry_3 = Entry(login_success_screen,textvariable=registrationid)
    entry_3.place(x=440,y=230)

    label_4 = Label(login_success_screen, text="Gender",width=20,font=("bold", 10))
    label_4.place(x=250,y=280)
    var = IntVar()
    Radiobutton(login_success_screen, text="Male",padx = 5, variable=var, value=1).place(x=445,y=280)
    Radiobutton(login_success_screen, text="Female",padx = 20, variable=var, value=2).place(x=500,y=280)
    label_5 = Label(login_success_screen, text="Email",width=20,font=("bold", 10))
    label_5.place(x=250,y=330)
    email=StringVar()
    entry_5 = Entry(login_success_screen,textvariable=email,width=40)
    entry_5.place(x=440,y=330)
   
    Button(login_success_screen, text='Submit',width=20,bg='brown',fg='white',command=datasave).place(x=400,y=480)

    login_success_screen.mainloop()
    
#==========================================================================================================================================================

# Designing popup for login invalid password
 
def password_not_recognised():
    global password_not_recog_screen
    password_not_recog_screen = Toplevel(login_screen)
    password_not_recog_screen.title("Success")
    password_not_recog_screen.geometry("100x100")
    Label(password_not_recog_screen, text="Invalid Password ").pack()
    Button(password_not_recog_screen, text="OK", command=delete_password_not_recognised).pack()
 
# Designing popup for user not found
 
def user_not_found():
    global user_not_found_screen
    user_not_found_screen = Toplevel(login_screen)
    user_not_found_screen.title("Success")
    user_not_found_screen.geometry("100x100")
    Label(user_not_found_screen, text="User Not Found").pack()
    Button(user_not_found_screen, text="OK", command=delete_user_not_found_screen).pack()



def delete_login_success():
    login_success_screen.destroy()
def delete_password_not_recognised():
    password_not_recog_screen.destroy()
 
 
def delete_user_not_found_screen():
    user_not_found_screen.destroy()

def main_account_screen():
    global main_screen
    main_screen = Tk()
    main_screen.geometry("1300x800")
    main_screen.title("Account Login")
    lblinfo = Label(font=( 'aria' ,30, 'bold' ),text="Online Parking System",fg="steel blue",bd=10).pack()
    i=ImageTk.PhotoImage(Image.open("lpu bg1.jpg"))
    Label(image=i,height=700,width=1600).pack()
    #lblinfo.place(x=400,y=10)
    b=Button(text="Login", height="2", width="30", command = login)
    b.place(x=550,y=200)
    c=Button(text="Register", height="2", width="30", command=register)
    c.place(x=550,y=250)
    main_screen.mainloop()
main_account_screen()

from tkinter import *
import tkinter as tk
global username
global password
global username_entry
global password_entry
global main_screen
main_screen = Tk()   # create a GUI window     

# define login function
def login():
    
    login_screen = Toplevel(main_screen)
    login_screen.title("Login")
    login_screen.geometry("300x250")
    Label(login_screen, text="Please enter details below to login").pack()
    Label(login_screen, text="").pack()
 
    global username_verify
    global password_verify
 
    username_verify = StringVar()
    password_verify = StringVar()
 
   
    Label(login_screen, text="Username * ").pack()
    username_login_entry = Entry(login_screen, textvariable=username_verify)
    username_login_entry.pack()
    Label(login_screen, text="").pack()
    Label(login_screen, text="Password * ").pack()
    password_login_entry = Entry(login_screen, textvariable=password_verify, show= '*')
    password_login_entry.pack()
    Label(login_screen, text="").pack()
    Button(login_screen,text="Login").pack()
   # Label(login_screen, text="").pack()
    #Button(login_screen, text="Login", width=10, height=1, command=login_verification).pack()
    

def register():
        
    register_screen = Toplevel(main_screen) 
    register_screen.title("Register")
    register_screen.geometry("300x280")
 
 # Set text variables
    name = StringVar()
    phonenumber = IntVar()
    email = StringVar()   
    username = StringVar()
    password = StringVar()
 
 # Set label for user's instruction
    Label(register_screen, text="Please enter details below", bg="blue").pack()
   # Label(register_screen, text="").pack()

# Set username label
    name_lable = Label(register_screen, text="name * ")
    name_lable.pack()
    
    name_entry = Entry(register_screen, textvariable=name)
    name_entry.pack()
    # Set username label
    phonenumber_lable = Label(register_screen, text="Phone number * ")
    phonenumber_lable.pack()
 
  
    phonenumber_entry = Entry(register_screen, textvariable=phonenumber)
    phonenumber_entry.pack()
    # Set username label
    email_lable = Label(register_screen, text="Email * ")
    email_lable.pack()
 
 # Set username entry
# The Entry widget is a standard Tkinter widget used to enter or display a single line of text.
    
    email_entry = Entry(register_screen, textvariable=email)
    email_entry.pack()

# Set username label
    username_lable = Label(register_screen, text="Username * ")
    username_lable.pack()

    username_entry = Entry(register_screen, textvariable=username)
    username_entry.pack()
   
 # Set password label
    password_lable = Label(register_screen, text="Password * ")
    password_lable.pack()
    
# Set password entry
    password_entry = Entry(register_screen, textvariable=password, show='*')
    password_entry.pack()
    
    Label(register_screen, text="").pack()
 
    Button(register_screen, text="Register", width=10, height=1, bg="blue").pack()

def main_account_screen():
  
    main_screen.geometry("300x270") # set the configuration of GUI window 
    main_screen.title("Account Login") # set the title of GUI window

# create a Form label 
Label(text="Choose Login Or Register For Parking", bg="blue", width="300", height="2", font=("Calibri", 13)).pack() 
Label(text="").pack() 

Button(text="Login", height="2", width="30", command = login).pack()

main_account_screen() 

Button(text="Register", height="2", width="30", command=register).pack() 
    
def register_user():
    username_entry=register()
main_screen.mainloop()
