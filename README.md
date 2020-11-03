# quiz-applicatcion
from tkinter import *
import os
import tkinter as tk
import final as mainPageGui

# Designing window for registration

def register():
    global register_screen
    register_screen = Toplevel(main_screen)
    register_screen.title("Register")
    register_screen.geometry("1400x1000")
    canvas = Canvas(register_screen,width=1300, height=800, bg='black')
    canvas.pack(expand=YES, fill=BOTH)
   
    gif1 = PhotoImage(file='19.png')
    canvas.create_image(0, 0, image=gif1, anchor=NW)

    global username
    global password
    global username_entry
    global password_entry
    username = StringVar()
    password = StringVar()
    f1=Frame(canvas,width=800,height=500,)
    f1.pack(side=TOP,padx=50,pady=250)
    Label(f1, text="Please enter details below", font=("TimesNewRoman",50),bg="blue").pack()
    Label(f1, text="").pack()
    username_lable = Label(f1, text="Username * ",font=("TimesNewRoman",20))
    username_lable.pack()
    username_entry = Entry(f1, textvariable=username)
    username_entry.pack()
    password_lable = Label(f1, text="Password * ",font=("TimesNewRoman",20))
    password_lable.pack()
    password_entry = Entry(f1, textvariable=password, show='*')
    password_entry.pack()
    Label(f1, text="").pack()
    Button(f1, text="Register", width=10, height=1,bd=4,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green", command = register_user).pack()
    register_screen.mainloop()


# Designing window for login 

def login():
    global login_screen
    login_screen = Toplevel(main_screen)
    login_screen.title("Login")
    login_screen.geometry("1400x1000")
    canvas = Canvas(login_screen,width=1300, height=800, bg='black')
    canvas.pack(expand=YES, fill=BOTH)
   
    gif1 = PhotoImage(file='19.png')
    canvas.create_image(0, 0, image=gif1, anchor=NW)
    f1=Frame(canvas,width=800,height=500,)
    f1.pack(side=TOP,padx=50,pady=250)
    Label(f1, text="Please enter details below to login",font=("TimesNewRoman",20)).pack()
    Label(f1, text="").pack()

    global username_verify
    global password_verify

    username_verify = StringVar()
    password_verify = StringVar()

    global username_login_entry
    global password_login_entry

    Label(f1, text="Username * ",font=("TimesNewRoman",20)).pack()
    username_login_entry = Entry(f1, textvariable=username_verify)
    username_login_entry.pack()
    Label(f1, text="").pack()
    Label(f1, text="Password * ",font=("TimesNewRoman",20)).pack()
    password_login_entry = Entry(f1, textvariable=password_verify, show= '*')
    password_login_entry.pack()
    Label(f1, text="").pack()
    Button(f1, text="Login", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green", command = login_verify).pack()
    login_screen.mainloop()
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

    Label(register_screen, text="Registration Success", fg="green", font=("calibri", 13)).pack()

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
def main_page_gui():
    mainPageGui.show()

def login_sucess():
    def delete_login_success():
        login_success_screen.destroy()
        main_page_gui()
    global login_success_screen
    login_success_screen = Toplevel(login_screen)
    login_success_screen.title("Success")
    login_success_screen.geometry("150x100")
    Label(login_success_screen, text="Login Success").pack()
    Button(login_success_screen, text="OK", command=delete_login_success).pack()
    

# Designing popup for login invalid password

def password_not_recognised():
    global password_not_recog_screen
    password_not_recog_screen = Toplevel(login_screen)
    password_not_recog_screen.title("Success")
    password_not_recog_screen.geometry("150x100")
    Label(password_not_recog_screen, text="Invalid Password ").pack()
    Button(password_not_recog_screen, text="OK", command=delete_password_not_recognised).pack()

# Designing popup for user not found
 
def user_not_found():
    global user_not_found_screen
    user_not_found_screen = Toplevel(login_screen)
    user_not_found_screen.title("Success")
    user_not_found_screen.geometry("150x100")
    Label(user_not_found_screen, text="User Not Found").pack()
    Button(user_not_found_screen, text="OK", command=delete_user_not_found_screen).pack()

# Deleting popups




def delete_password_not_recognised():
    password_not_recog_screen.destroy()


def delete_user_not_found_screen():
    user_not_found_screen.destroy()


# Designing Main(first) window

def main_account_screen():
    global main_screen
    main_screen = Tk()
    main_screen.geometry("1400x1000")
    main_screen.title("Account Login")
    canvas = Canvas(main_screen,width=1300, height=800, bg='black')
    canvas.pack(expand=YES, fill=BOTH)
   
    gif1 = PhotoImage(file='19.png')
    canvas.create_image(0, 0, image=gif1, anchor=NW)
    f2=Frame(canvas,width=800,height=500,)
    f2.pack(side=TOP,padx=50,pady=250)
    Label(f2,text="Select Your Choice", bg="blue", width="300", height="2", font=("Calibri", 30)).pack()
    Label(f2,text="").pack()
    Button(f2,text="Login", height="2", width="30", bd=4,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command = login).pack()
    Label(f2,text="").pack()
    Button( f2,text="Register", height="2", width="30",bd=4,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green", command=register).pack()

    main_screen.mainloop()


main_account_screen()
from tkinter import*
from tkinter import messagebox
import tkinter as tk

#from tkinter import fileframe2
def show():
    i=0
    root=Toplevel()
    root.title("quiz application")
    width = root.winfo_screenwidth()
    height = root.winfo_screenheight()
    root.geometry(f'{width}x{height}')
    root.config(bg='grey')
    #root.geometry("1400x1000")
    #root.config(bg='grey')

    canvas = Canvas(root,width=0, height=0, bg='black')
    canvas.pack(expand=YES, fill=BOTH)
    gif1 = PhotoImage(file='3.png')

    canvas.create_image(0, 0, image=gif1, anchor=NW)


    f=Frame(canvas,width=1300,height=400,bg='black')
    f.pack(side=TOP, pady=0)
    L=Label(f,text="!!!Welcome!!!  ",font=('Lucida Handwriting',50,'bold'),fg='blue4',bg='pink')
    L.pack()

    f3=Frame(canvas,width=1300,height=400)
    f3.pack(side=BOTTOM,padx=0,pady=150)
    print("sravntj")
    score=0;
    file = open('score1.txt','w')
    file.write(str(score))
    def calculateScore(currentScore):
        file = open('score1.txt','r')
        try:
            score=int(file.read().strip())
        except:
            score=0

        print("before")
        print(score)
        score=score+currentScore
        print("after:")
        print(score)
        file = open('score1.txt','w')
        file.write(str(score))
        file.close()
    def returnTotalScore():
        return int(score)

    def frame9():
        frame9 = Toplevel()
        frame9.geometry("1400x1000")
        canvas = Canvas(frame9,width=1300, height=900, bg='black')
        


        
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='10.png')
        canvas.create_image(0, 0, image=gif1, anchor=NW)
        root.mainloop()
    def frame8():
        def mmm():
            file = open('score1.txt','r')
            try:
                score=int(file.read().strip())
            except:
                score=0
            return score
            

        
            
        def get_frame9():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame8.destroy()
            frame9()
        frame8 = Toplevel()
        frame8.geometry("1400x1000")
        canvas = Canvas(frame8,width=1300, height=900, bg='black')

        
        canvas.pack(expand=YES, fill=BOTH)
        f2=Frame(canvas,width=1300,height=900)
        f2.pack(side=TOP,padx=50)
        gif1 = PhotoImage(file='12.png')
        canvas.create_image(0, 0, image=gif1, anchor=NW)
        f3=Frame(canvas,width=1300,height=500)
        f3.pack(side=RIGHT,padx=0,pady=0)
        f4=Frame(canvas,width=700,height=200)
        f4.pack(side=LEFT,padx=0,pady=0)
        print(mmm())
        score=mmm()
        b1=Button(f3, text="NEXT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame9)
        b1.grid(row=10,column=10)
        b2=Button(f4, text=score, bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green")
        b2.grid( row=10,column=10)
        gif2 = PhotoImage(file='SCORE_logo.png')
        se1=Button(f2,image=gif2,bd=10,width=500,height=180,bg="orange")
        se1.grid(row=10,column=10)
        se1.pack(side=TOP)
        root.mainloop()

    def frame7():

        def ShowChoice():
            a = (v.get())
            if (a==0):
                score = 100
            else:
                score = -50
            calculateScore(score)
        def get_frame8():
            ShowChoice()
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame7.destroy()
            frame8()
        def quit5():
            
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame7.destroy()
            frame8()   
        frame7 = Toplevel()
        frame7.geometry("1400x1000")
        canvas = Canvas(frame7,width=1300, height=900, bg='black')
        
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='4.png')
        #cover = resizeimage.resizecover(image,[200,100], validate = false)
        f1=Frame(canvas,width=800,height=500,)
        f1.pack(side=TOP,padx=50,pady=250)


        canvas.create_image(10 ,20, image=gif1, anchor=NW)

        v = tk.IntVar()
        v.set(1)  # initializing the choice, i.e. Python

        options5 = [
            ("1 point"),
            (" 2 point"),
            ("3 point"),
            (" none of these"),
            
        ]


        

        tk.Label(f1, 
                 text=""" A free throw is worth of""",font =("Lucid",20),
                 justify = tk.CENTER,
                 padx = 90).pack(anchor=tk.CENTER)

        for val, option in enumerate(options5):
            tk.Radiobutton(f1, 
                          text=option,
                           indicatoron = 0,
                           font =("Lucid",20),
                          width = 20,
                          padx = 90,
                          variable=v,
                          value=val).pack(anchor=tk.CENTER)
        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=RIGHT,padx=100,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame8)
        b1.grid(row=10,column=10)
        f4=Frame(canvas,width=100,height=50)
        f4.pack(side=LEFT,padx=100,pady=0)
        b2=Button(f4, text="QUIT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='green',state='normal',bg="red",command=quit5)
        b2.grid(row=10,column=10)


        root.mainloop()

        
    def frame6():
        def ShowChoice():
            a = (v.get())
            
            if (a==0):
                score =100
            else:
                score = -50
            calculateScore(score)

        
        def get_frame7():
            ShowChoice()
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame6.destroy()
            frame7()
        def quit4():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame6.destroy()
            frame8()   
        frame6 = Toplevel()
        frame6.geometry("1400x1000")
        canvas = Canvas(frame6,width=1300, height=900, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='4.png')
        #cover = resizeimage.resizecover(image,[200,100], validate = false)
        f1=Frame(canvas,width=800,height=500,)
        f1.pack(side=TOP,padx=50,pady=250)


        canvas.create_image(10 ,20, image=gif1, anchor=NW)

        v = tk.IntVar()
        v.set(1)  # initializing the choice, i.e. Python

        options4= [
            ("james naismith"),
            (" willian morgan"),
            (" jim thorpe"),
            (" none of these"),
            
        ]



        tk.Label(f1, 
                 text=""" Who made basketball""",font =("Lucid",20),
                 justify = tk.CENTER,
                 padx = 90).pack(anchor=tk.CENTER)

        for val, option in enumerate(options4):
            tk.Radiobutton(f1, 
                          text=option,
                           indicatoron = 0,
                           font =("Lucid",20),
                          width = 20,
                          padx = 90,
                          variable=v,
                          value=val).pack(anchor=tk.CENTER)
        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=RIGHT,padx=100,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame7)
        b1.grid(row=10,column=10)
        f4=Frame(canvas,width=100,height=50)
        f4.pack(side=LEFT,padx=100,pady=0)
        b2=Button(f4, text="QUIT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='green',state='normal',bg="red",command=quit4)
        b2.grid(row=10,column=10)

        root.mainloop()


        
        
    def frame5():    
        def ShowChoice():
            a = (v.get())
            if (a==2):
                score = 100
            else:
                score = -50
            calculateScore(score)


        def get_frame6():
            ShowChoice()
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            
            
            frame5.destroy()
            frame6()
        def quit3():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame5.destroy()
            frame8()
            
        frame5 = Toplevel()
        frame5.geometry("1400x1000")
        canvas = Canvas(frame5,width=1300, height=900,bg='black')
        gif1 = PhotoImage(file='4.png')
        canvas.pack(expand=YES, fill=BOTH)
        
         
        #cover = resizeimage.resizecover(image,[200,100], validate = false)
        f1=Frame(canvas,width=800,height=500)
        f1.pack(side=TOP,padx=50,pady=250)
        canvas.create_image(10 ,20, image=gif1,anchor=NW)

        v = tk.IntVar()
        v.set(1)  # initializing the choice, i.e. Python

        options3 = [
            ("Euroleague"),
            (" NIBA"),
            ("FIBA"),
            (" none of these"),
            
        ]

        def ShowChoice():
            a = (v.get())
            if (a==2):
                score = 100
            else:
                score = -50
            calculateScore(score)

        

        tk.Label(f1, 
                 text="""What is the highest governing body of basket ball?""",font =("Lucid",20),
                 justify = tk.CENTER,
                 padx = 90).pack(anchor=tk.CENTER)

        for val, option in enumerate(options3):
            tk.Radiobutton(f1, 
                          text=option,
                           indicatoron = 0,
                           font =("Lucid",20),
                          width = 20,
                          padx = 90,
                          variable=v,
                          value=val).pack(anchor=tk.CENTER)

        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=RIGHT,padx=100,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame6)
        b1.grid(row=10,column=10)
        f4=Frame(canvas,width=100,height=50)
        f4.pack(side=LEFT,padx=100,pady=0)
        b2=Button(f4, text="QUIT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='green',state='normal',bg="red",command=quit3)
        b2.grid(row=10,column=10)
        root.mainloop()

    def frame4():
        def ShowChoice():
            a = (v.get())
            if (a==2):
                score = 100
            else:
                score = -50
            calculateScore(score)
            file = open('score.txt','w')
            file.write(str(score))

        def get_frame5():
            ShowChoice()
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame4.destroy()
            frame5()
        def quit2():
            ShowChoice();
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame4.destroy()
            frame8()
        
       
        frame4 = Toplevel()
        frame4.geometry("1400x1000")
        canvas = Canvas(frame4,width=1300, height=900, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
         
        gif1 = PhotoImage(file='4.png')
        #cover = resizeimage.resizecover(image,[200,100], validate = false)
        f1=Frame(canvas,width=800,height=500)
        f1.pack(side=TOP,padx=50,pady=250)


        canvas.create_image(10 ,20, image=gif1, anchor=NW)

        v = tk.IntVar()
        v.set(1)  # initializing the choice, i.e. Python

        options2 = [
            ("1737"),
            (" 1974"),
            ("1891"),
            (" none of these"),
            
        ]


        

        tk.Label(f1, 
                 text="""When was baketball made?""",font =("Lucid",20),
                 justify = tk.CENTER,
                 padx = 90).pack(anchor=tk.CENTER)

        for val, option in enumerate(options2):
            tk.Radiobutton(f1, 
                          text=option,
                           indicatoron = 0,
                           font =("Lucid",20),
                          width = 20,
                          padx = 90,
                          variable=v,
                          value=val).pack(anchor=tk.CENTER)
        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=RIGHT,padx=100,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame5)
        b1.grid(row=10,column=10)
        f4=Frame(canvas,width=100,height=50)
        f4.pack(side=LEFT,padx=100,pady=0)
        b2=Button(f4, text="QUIT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='green',state='normal',bg="red",command=quit2)
        b2.grid(row=10,column=10)


        root.mainloop()

        
    def frame1():
        frame1=Toplevel()
        frame1.geometry(f'{width}x{height}')
        frame1.config(bg='grey')

        canvas = Canvas(frame1,width=0, height=0, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='3.png')

        canvas.create_image(0, 0, image=gif1, anchor=NW)


        f=Frame(canvas,width=1300,height=400,bg='black')
        f.pack(side=TOP, pady=0)
        L=Label(f,text="WELCOME !!! it's ",font=('Lucida Handwriting',50,'bold'),fg='blue4',bg='pink')
        L.pack()
        f3=Frame(canvas,width=1300,height=400)
        f3.pack(side=BOTTOM,padx=0,pady=150)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame2)
        b1.grid(row=10,column=10)
        frame1.mainloop()
    def frame3():
        def ShowChoice():
            a = (v.get())
            print(a)
            if (a==1):
                score =100
            else:
                score= -50
            calculateScore(score)
        def get_frame4():
            ShowChoice()
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame3.destroy()
            frame4()
        def quit1():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame3.destroy()
            frame8()
            
            
             
        
        frame3 = Toplevel()
        frame3.geometry("1400x1000")
        canvas = Canvas(frame3,width=1300, height=900, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='4.png')
        #cover = resizeimage.resizecover(image,[200,100], validate = false)
        f1=Frame(canvas,width=800,height=500,)
        f1.pack(side=TOP,padx=50,pady=250)


        canvas.create_image(10 ,20, image=gif1, anchor=NW)

        v = tk.IntVar()
        v.set(1)  # initializing the choice, i.e. Python

        options1 = [
            ("5 players"),
            (" 10 players"),
            ("15 players"),
            (" none of these"),
            
        ]

       

        tk.Label(f1,
                 text="""There are total _________ players on the basketball at one time""",font =("Lucid",20),
                 justify = tk.CENTER,
                 padx = 90).pack(anchor=tk.CENTER)

        for val, option in enumerate(options1):
            tk.Radiobutton(f1, 
                          text=option,
                           indicatoron = 0,
                           font =("Lucid",20),
                          width = 20,
                          padx = 90,
                          variable=v,
                          value=val).pack(anchor=tk.CENTER)
        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=RIGHT,padx=100,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame4)
        b1.grid(row=10,column=10)
        f4=Frame(canvas,width=100,height=50)
        f4.pack(side=LEFT,padx=100,pady=0)
        b2=Button(f4, text="QUIT", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='green',state='normal',bg="red",command=quit1)
        b2.grid(row=10,column=10)


        frame3.mainloop()
        
    def frame2():
        def get_frame3():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame2.destroy()
            frame3()

        import winsound
        winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
        frame2=Toplevel()
        frame2.geometry("1400x1000")
        frame2.config(bg='grey')

        canvas= Canvas(frame2,width=0, height=0, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='13.png')

        canvas.create_image(0,0, image=gif1, anchor=NW)


        f01=Frame(canvas,width=1300,height=400,bg='black')
        f01.pack(side=BOTTOM, pady=80,padx=260)
        tk.Label(f01, text= 'Strict rules of quiz that need to followed:\n'
                                        '==>QUIT button will end the quiz\n '
                                        '==>Correct answer100 points are rewarded\n'
                                        '==>Wrong answer 50 will be deducted fro your score\n'
                                        '==> NEXT button will get into next question',font=('Lucida Handwriting',20,'bold'),fg='blue4',bg='pink',padx = 90).pack(anchor=tk.CENTER)

        #f03=Frame(canvas,width=100,height=40)
        #f03.pack(side=RIGHT,padx=200)
        from tkinter import messagebox
        #f3=Frame(canvas,width=2400,height=500)
        f3=Frame(canvas,width=2400,height=500)
        f3.pack(side=BOTTOM,padx=0,pady=0)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame3)
        b1.grid(row=10,column=10)
        frame2.mainloop()
    def get0() :
        def get_frame2():
            import winsound
            winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
            frame1.destroy()
            frame2()
        import winsound
        winsound.PlaySound("slide.wav", winsound.SND_ASYNC)
        frame1=Toplevel()
        frame1.geometry(f'{width}x{height}')
        frame1.config(bg='grey')

        canvas = Canvas(frame1,width=0, height=0, bg='black')
        canvas.pack(expand=YES, fill=BOTH)
        gif1 = PhotoImage(file='3.png')

        canvas.create_image(0, 0, image=gif1, anchor=NW)


        f=Frame(canvas,width=1300,height=400,bg='black')
        f.pack(side=TOP, pady=0)
        L=Label(f,text="WELCOME !!! it's ",font=('Lucida Handwriting',50,'bold'),fg='blue4',bg='pink')
        L.pack()
        f3=Frame(canvas,width=1300,height=400)
        f3.pack(side=BOTTOM,padx=0,pady=150)
        b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=get_frame2)
        b1.grid(row=10,column=10)
        frame1.mainloop()

    b1=Button(f3, text="Next", bd=4,width=8,font=("TimesNewRoman",20),relief='flat',activebackground='red',state='normal',bg="green",command=frame2)
    b1.grid(row=10,column=10)
    root.mainloop()
    #root1.mainloop()

